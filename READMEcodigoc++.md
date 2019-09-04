#include <time.h>
#include<stdint.h>
#include<stdlib.h>
#include <iostream>
#include <windows.h>
#define TAM 100000
#define TAMMATRIZ 225


int main()
{
	void UTF_8();
	void bubble_sort(int vetor[]);
	void selection_sort(int vetor[]);
	void insertion_sort(int V[]);
	void busca_sequencial(int vetor[], int valor);
	int busca_binario(int vetor[], int valor);
	void multiplica_matriz(long m1[TAMMATRIZ][TAMMATRIZ], long m2[TAMMATRIZ][TAMMATRIZ]);
	UTF_8();
	int opc;
	int vetor [TAM];
	long m1[TAMMATRIZ][TAMMATRIZ];
	long m2[TAMMATRIZ][TAMMATRIZ];

	printf("\n1-Ordenar vetor\n2-Buscar valor no vetor\n3-Multiplicar 2 matrizes\nEscolha a opção: ");
	scanf_s(" %d",&opc);
	if (opc == 1) {
		for (int i = 0; i < TAM; i++) {
			vetor[i] = TAM - i;
		}
		printf("1-Método da bolha\n2-Método de Seleção\n3-Método de Inserção\nEscolha a opção: ");
		scanf_s("%d", &opc);
		if (opc == 1) {	
			bubble_sort(vetor);	
		}
		else if (opc == 2) {
			selection_sort(vetor);	
		}
		else if (opc == 3) {
			insertion_sort(vetor);
		}

	}
	else if (opc == 2) {
		for (int i = 0; i < TAM; i++) {
			vetor[i] = i+1;
		}
		int valor;
		printf("Qual o valor deseja buscar no vetor: ");
		scanf_s("%d", &valor);
		printf("1-Busca sequencial\n2-Busca binária\nEscolha a opção: ");
		scanf_s("%d",&opc);
		if (opc == 1) {
			busca_sequencial(vetor, valor);
		}
		else if (opc == 2) {
			clock_t Ticks[2];
			Ticks[0] = clock();
			int meio = busca_binario(vetor, valor);
			printf("O valor %d está no índice %d", valor, meio);
			Ticks[1] = clock();
			double Tempo = (Ticks[1] - Ticks[0]) * 1000.0 / CLOCKS_PER_SEC;
			printf("\nTempo gasto: %g ms.", Tempo);
		}
	}
	else if (opc == 3) {
		long contador = 1;
		for (int i = 0; i < TAMMATRIZ; i++) {
			for (int j = 0; j < TAMMATRIZ; j++) {
				m1[i][j] = contador++;
			}
		}
		contador = 1;
		for (int i = 0; i < TAMMATRIZ; i++) {
			for (int j = 0; j < TAMMATRIZ; j++) {
				m2[i][j] = contador++;
			}
		}
		multiplica_matriz(m1, m2);
	}
	
	return 0;
}
void UTF_8() {
	UINT CPAGE_UTF8 = 65001;
	UINT CPAGE_DEFAULT = GetConsoleOutputCP();
	SetConsoleOutputCP(CPAGE_UTF8);
}
void bubble_sort(int vetor[]) {
	clock_t Ticks[2];
	Ticks[0] = clock();
	int k, j, i, aux;
	for (k = 1; k < TAM; k++) {
		for (j = 0; j < TAM - 1; j++) {
			if (vetor[j] > vetor[j + 1]) {
				aux = vetor[j];
				vetor[j] = vetor[j + 1];
				vetor[j + 1] = aux;
			}
		}
	}
	Ticks[1] = clock();
	double Tempo = (Ticks[1] - Ticks[0]) * 1000.0 / CLOCKS_PER_SEC;
	
	for (i = 0; i < TAM; i++) {
		printf("%d ", vetor[i]);
	}
	printf("\nTempo gasto: %g ms.", Tempo);
}
void selection_sort(int vetor[]) {
	clock_t Ticks[2];
	Ticks[0] = clock();
	for (int indice = 0; indice < TAM; ++indice) {
		int indiceMenor = indice;
		for (int indiceSeguinte = indice + 1; indiceSeguinte < TAM; ++indiceSeguinte) {
			if (vetor[indiceSeguinte] < vetor[indiceMenor]) {
				indiceMenor = indiceSeguinte;
			}
		}
		int aux = vetor[indice];
		vetor[indice] = vetor[indiceMenor];
		vetor[indiceMenor] = aux;
	}
	Ticks[1] = clock();
	double Tempo = (Ticks[1] - Ticks[0]) * 1000.0 / CLOCKS_PER_SEC;
	for (int i = 0; i < TAM; i++) {
		printf("%d ", vetor[i]);
	}
	printf("\nTempo gasto: %g ms.", Tempo);
}
void insertion_sort(int vetor[]) {
	clock_t Ticks[2];
	Ticks[0] = clock();
	for (int i = 1; i < TAM; i++) {
		int escolhido = vetor[i];
		int j = i - 1;

		while ((j >= 0) && (vetor[j] > escolhido)) {
			vetor[j + 1] = vetor[j];
			j--;
		}

		vetor[j + 1] = escolhido;
	}
	Ticks[1] = clock();
	double Tempo = (Ticks[1] - Ticks[0]) * 1000.0 / CLOCKS_PER_SEC;
	for (int a = 0; a < TAM; a++) {
		printf("%d ", vetor[a]);
	}
	printf("\nTempo gasto: %g ms.", Tempo);
}
void busca_sequencial(int vetor[],int valor){
	clock_t Ticks[2];
	Ticks[0] = clock();
	for (int i = 0; i < TAM; i++) {
		if (valor == vetor[i]) {
			printf("O valor %d foi encontrado no índice %d",valor,i);
		}	
	}
	Ticks[1] = clock();
	double Tempo = (Ticks[1] - Ticks[0]) * 1000.0 / CLOCKS_PER_SEC;
	printf("\nTempo gasto: %g ms.", Tempo);
}
int busca_binario(int vetor[], int valor) {
	int primeiro, meio, ultimo;
	primeiro = 0;
	ultimo = TAM - 1;
	while (primeiro <= ultimo) {
		meio = (primeiro + ultimo) / 2;
		if (valor == vetor[meio]) {
			return meio;
		}
		else if (valor < meio) {
			ultimo = meio - 1;
		}
		else if (valor > meio) {
			primeiro = meio + 1;
		}
	}
}
void multiplica_matriz(long m1[TAMMATRIZ][TAMMATRIZ], long m2[TAMMATRIZ][TAMMATRIZ]) {
	clock_t Ticks[2];
	Ticks[0] = clock();
	long m3[TAMMATRIZ][TAMMATRIZ];
	int acumula = 0;
	for (int i = 0; i < TAMMATRIZ; i++) {
		for (int j = 0; j < TAMMATRIZ; j++) {
			for (int k = 0; k < TAMMATRIZ; k++) {
				acumula = acumula + (m1[i][k] * m2[k][j]);
				m3[i][j] = acumula;
			}
			acumula = 0;
		}
	}
	Ticks[1] = clock();
	double Tempo = (Ticks[1] - Ticks[0]) * 1000.0 / CLOCKS_PER_SEC;
	for (int i = 0; i < TAMMATRIZ; i++) {
		for (int j = 0; j < TAMMATRIZ; j++) {
			printf("%u ", m3[i][j]);
		}
		printf("\n");
	}
	printf("\nTempo gasto: %g ms.", Tempo);
}
