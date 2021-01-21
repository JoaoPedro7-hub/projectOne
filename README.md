# projectOne
package SegundoGQ;
import java.util.Scanner;

public class ValidandoCPF {
	public static int calcularDigitoVerificador(String cpf, int [] veri, int cond) {
		int i, valor,  soma = 0, resto;
		for (i = 0; i < cond; i++) {
			valor = cpf.charAt(i) - '0';
			soma = soma + (valor * veri[i]);
		}
		resto = soma % 11;
		if (resto < 2) {
			return 0;
		}
		else {
			return 11 - resto;
		}
	}
	public static boolean validando(String cpf) {//função de validação do CPF
		int tamanho, i, dig1, dig2;
		int [] veri = new int [10];
		char car;
		
		preencherVetor(veri, 10, 9);
		tamanho = cpf.length();
		if(tamanho != 11) {
			return false;
		}
		else {
			for (i = 0; i < tamanho; i++) {
				car = cpf.charAt(i);
				if(Character.isDigit(car) == false) {
					return false;
				}
			}
			dig1 = calcularDigitoVerificador(cpf, veri, 9);
			preencherVetor(veri, 11, 10);
			dig2 = calcularDigitoVerificador(cpf, veri, 10);
			
			if(dig1 != cpf.charAt(9) - '0' || dig2 != cpf.charAt(10) - '0') { 
				return false;
			}
		}
		return true;
	}
	
	public static void preencherVetor (int [] veri, int valor, int cond) {
		int i;
		for (i = 0; i < cond; i++) {
			veri[i] = valor - i;
		}
	}
	public static void main(String[] args) {
		Scanner s = new Scanner(System.in);
		String resposta, condition = ("sim"), condition2 = ("não");
		int tam;
		
		do {
			String cpf;
			boolean result;
			System.out.println("Informe o CPF a ser validade:");
			cpf = s.nextLine();cpf = s.nextLine();
			result = validando(cpf);
			
			if(result == true) {
				System.out.println("\nO Cpf informado é válido!");
			}
			else {
				System.out.println("\nO Cpf informado é inválido!");
			}
			System.out.println("Deseja validar mais algum Cpf?" +
					"\nDigite Sim para continuar e Não para encerrar o Programa!");
			resposta = s.nextLine();
			while(resposta.equalsIgnoreCase(condition) == false && resposta.equalsIgnoreCase(condition2) == false) {
			System.out.println("Resposta inválida. Digite Sim para continuar ou Não para encerrar o programa.");
			resposta = s.nextLine();
		}
	} while (resposta.equalsIgnoreCase(condition) == true);
}
}
