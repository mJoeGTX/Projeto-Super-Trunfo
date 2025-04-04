#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <string.h>

#define NUM_CAPITAIS 5  // Pode expandir depois

typedef struct {
    char nome[50];
    int populacao; // em mil habitantes
    float densidade; // hab/km²
    float pib; // em bilhões de reais
} Capital;

// Lista de algumas capitais
Capital capitais[NUM_CAPITAIS] = {
    {"São Paulo", 12300, 7398.26, 230.0},
    {"Rio de Janeiro", 6770, 5265.82, 160.0},
    {"Brasília", 3090, 444.66, 140.0},
    {"Salvador", 2887, 3683.40, 63.0},
    {"Fortaleza", 2680, 7794.76, 67.0}
};

// Função para exibir carta
void mostrarCarta(Capital c) {
    printf("\n--- %s ---\n", c.nome);
    printf("1. População: %d mil hab\n", c.populacao);
    printf("2. Densidade: %.2f hab/km²\n", c.densidade);
    printf("3. PIB: R$ %.2f bilhões\n", c.pib);
}

// Função para comparar o atributo escolhido
void comparar(Capital jogador, Capital computador, int atributo) {
    float valorJogador, valorComputador;

    switch (atributo) {
        case 1:
            valorJogador = jogador.populacao;
            valorComputador = computador.populacao;
            break;
        case 2:
            valorJogador = jogador.densidade;
            valorComputador = computador.densidade;
            break;
        case 3:
            valorJogador = jogador.pib;
            valorComputador = computador.pib;
            break;
        default:
            printf("Atributo inválido.\n");
            return;
    }

    printf("\nVocê: %.2f | Computador: %.2f\n", valorJogador, valorComputador);

    if (valorJogador > valorComputador)
        printf("🎉 Você venceu esse turno!\n");
    else if (valorJogador < valorComputador)
        printf("💻 O computador venceu esse turno!\n");
    else
        printf("⚖️ Empate!\n");
}

int main() {
    srand(time(NULL));

    int indiceJogador = rand() % NUM_CAPITAIS;
    int indiceComputador = rand() % NUM_CAPITAIS;

    while (indiceComputador == indiceJogador) {
        indiceComputador = rand() % NUM_CAPITAIS;
    }

    Capital cartaJogador = capitais[indiceJogador];
    Capital cartaComputador = capitais[indiceComputador];

    printf("Sua carta:");
    mostrarCarta(cartaJogador);

    int escolha;
    printf("\nEscolha o atributo para disputar (1 - População, 2 - Densidade, 3 - PIB): ");
    scanf("%d", &escolha);

    printf("\nCarta do Computador:");
    mostrarCarta(cartaComputador);

    comparar(cartaJogador, cartaComputador, escolha);

    return 0;
}
