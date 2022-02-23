# JAVA
Códigos para desafio 



1) package br.com.capgemini.desafio.funcoes;

import java.util.Scanner;

public class QuestaoUm {

public static void main(String[] args) {
	/**
	 * Método main chama o método montaEscada() e retorna sua resposta;
	 * 
	 * @param int numero define a quantide de linhas(*) que formarão a escada
	 * @return String escadaMontada retorna o desenho da escada
	 */
	int numero;
	String escadaMontada;
	Scanner scanner = new Scanner(System.in);

	System.out.print("Digite um tamanho numérico para forma sua escada: ");
	numero = scanner.nextInt();
	escadaMontada = montaEscada(numero);

	System.out.println(escadaMontada);

}

public static String montaEscada(int numero) {
	/**
	 * Método montaEscada() realiza um laço for através do iterador a, que é o
	 * responsável por verificar qual linha da escada esta sendo construida e
	 * adicionar espaços e asteriscos até que o tamanho final seja atingido.
	 * 
	 * @return String escada retorna o desenho da escada
	 * 
	 * O método repeat() é usado para retornar String cujo valor é a concatenação de
	 * determinadas vezes de contagem repetida de String.

	 */
	int a;
	String escada = "";

	for (a = 1; a <= numero; a++) {
		escada += " ".repeat(numero - a) + "*".repeat(a) + "\n";
	}

	return escada;
    }
    }
    
    2) 
package br.com.capgemini.desafio.funcoes;

import java.util.Scanner;
import java.util.regex.Pattern;

public class QuestaoDois {
/**
 * Método main chama o método validaSenha() e retorna sua resposta;
 * 
 * @param String senha recebe a palavra que será validada no metodo
 *               validaSenha()
 * @return int valor retorna um numero maior que 0 se a senha for validada como
 *         fraca ou 0 se a senha for validada como forte
 */
public static void main(String[] args) {

	String senha;
	int valor;
	Scanner scanner = new Scanner(System.in);

	System.out.print("Escreva sua senha: ");
	senha = scanner.next();
	valor = validaSenha(senha);

	System.out.println(valor);

}

/**
 * Método validaSenha() recebe uma string e análisa, através de expressões
 * regulares, se a senha é forte ( senha == 0) ou fraca ( senha > 0).
 * 
 * @param senhaMinuscula expressão regular que valida se a senha possui
 *                       caracteres minúsculos
 * @param senhaMaiuscula expressão regular que valida se a senha possui
 *                       caracteres maiúsculos
 * @param senhaDigito    expressão regular que valida se a senha possui
 *                       caracteres numéricos
 * @param senhaEspecial  expressão regular que valida se a senha possui
 *                       caracteres especiais
 * 
 * @param Boolean        para cada pattern -> Verdadeiro se cumpre os requisitos
 *                       do pattern -> Falso se não cumpre os requisitos do
 *                       pattern, adiciona 1 a x.
 * 
 * @return int x se o tamanho da senha mais o valor de x for maior que 6, senão
 *         retorna int y, indicando quantos digitos faltam para formar uma senha
 *         forte.
 * 
 */

public static Integer validaSenha(String senha) {
	int tamanho = senha.length();
	int x = 0;
	int y;
	boolean senhaMinuscula = Pattern.matches("^(?=.*[a-z]).+$", senha),
			senhaMaiuscula = Pattern.matches("^(?=.*[A-Z]).+$", senha),
			senhaDigito = Pattern.matches("^(?=.*\\d).+$", senha),
			senhaEspecial = Pattern.matches("^(?=.*[-+_!@#$%^&*.,?]).+$", senha);

	if (senhaMinuscula == false) {
		x += 1;
	}
	if (senhaMaiuscula == false) {
		x += 1;
	}
	if (senhaDigito == false) {
		x += 1;
	}
	if (senhaEspecial == false) {
		x += 1;
	}

	if (tamanho + x >= 6) {
		return x;
	} else {
		y = (6 - tamanho);
		return y;
	}

    }
}

3) package br.com.capgemini.desafio.funcoes;

import java.util.Arrays;
import java.util.HashMap;
import java.util.Scanner;

public class QuestaoTres {
/**
 * Método main chama o método montaParesAnagrama() e retorna sua resposta;
 * 
 * @param String palavra recebe a palavra que será analisada no método
 *               montaParesAnagrama()
 * 
 * @return int valor retorna o número de pares de anagrama da palavra digitada
 */

public static void main(String[] args) {

	String palavra;
	int valor;
	Scanner scanner = new Scanner(System.in);

	System.out.print("Digite uma palavra qualquer: ");
	palavra = scanner.next();
	valor = montaParesAnagrama(palavra);

	System.out.println(valor);
}

/**
 * Método montaParesAnagrama() recebe uma string e retorna a quantidade de pares
 * de anagramas que são possíveis formar a partir do input recebido.
 * 
 * A palavra recebida no método é transformada, através do laço for, em um array
 * com todos os possíveis pares de substring, e depois ordenado através do sort.
 * 
 * A estrutura boleana separa a quantidade de anagramas e as armazena junto a
 * sua chave no map.
 * 
 * Outro laço for é feito para definir os pares de anagramas e esse valor é
 * armazenado em paresAnagrama
 * 
 * @return int paresAnagrama retorna o valor de pares de anagramas encontrado na
 *         string palavra
 */
public static Integer montaParesAnagrama(String palavra) {

	HashMap<String, Integer> map = new HashMap<>();
	int a, b, tamanho = palavra.length();

	for (a = 0; a < tamanho; a++) {
		for (b = a; b < tamanho; b++) {
			char[] arrayPalavra = palavra.substring(a, b + 1).toCharArray();
			Arrays.sort(arrayPalavra);
			String chaveArrayPalavra = new String(arrayPalavra);
			if (map.containsKey(chaveArrayPalavra))
				map.put(chaveArrayPalavra, map.get(chaveArrayPalavra) + 1);
			else
				map.put(chaveArrayPalavra, 1);
		}
	}

	int paresAnagrama = 0;
	for (String chave : map.keySet()) {
		int x = map.get(chave);
		paresAnagrama += (x * (x - 1)) / 2; 
	}
	return paresAnagrama;
}
}
