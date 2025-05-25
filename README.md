#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_APARELHOS 10
#define MAX_NOME 50

typedef struct {
    char nome[MAX_NOME];
    float consumoEnergia;
    float consumoAgua;
    int prioridade;
} Aparelho;

void mostrarTabelaEstimativa() {
    printf("\nTabela de Consumo Estimado de Aparelhos:\n");
    printf("1. Geladeira: 15-20 kWh/mes\n");
    printf("2. Micro-ondas: 1-2 kWh/mes\n");
    printf("3. Chuveiro: 50-100 kWh/mes\n");
    printf("4. Maquina de Lavar: 10-30 kWh/mes\n");
    printf("5. Lava-louças: 10-20 kWh/mes\n\n");
}

void mochila(Aparelho aparelhos[], int n, float limiteAgua, float limiteEnergia) {
    float aguaUsada = 0, energiaUsada = 0;
    int i;
    printf("\nAparelhos Selecionados com Base na Prioridade e Limites:\n");
    for (i = 0; i < n; i++) {
        if (aguaUsada + aparelhos[i].consumoAgua <= limiteAgua &&
            energiaUsada + aparelhos[i].consumoEnergia <= limiteEnergia) {
            printf("Usar: %s | Água: %.1f L | Energia: %.1f kWh | Prioridade: %d\n",
                   aparelhos[i].nome, aparelhos[i].consumoAgua,
                   aparelhos[i].consumoEnergia, aparelhos[i].prioridade);
            aguaUsada += aparelhos[i].consumoAgua;
            energiaUsada += aparelhos[i].consumoEnergia;
        }
    }
    printf("Total utilizado: Agua = %.1f L | Energia = %.1f kWh\n", aguaUsada, energiaUsada);
}

int main() {
    Aparelho aparelhos[MAX_APARELHOS];
    int numAparelhos, i;
    float limiteAgua, limiteEnergia;

    mostrarTabelaEstimativa();

    printf("Informe a quantidade de aparelhos: ");
    scanf("%d", &numAparelhos);

    for (i = 0; i < numAparelhos; i++) {
        printf("\nAparelho %d:\n", i + 1);
        printf("Nome: ");
        scanf("%s", aparelhos[i].nome);
        printf("Consumo de Energia (kWh): ");
        scanf("%f", &aparelhos[i].consumoEnergia);
        printf("Consumo de Agua (L): ");
        scanf("%f", &aparelhos[i].consumoAgua);
        printf("Prioridade (1 - Muito Alta, 5 - Muito Baixa): ");
        scanf("%d", &aparelhos[i].prioridade);
    }

    printf("\nInforme o limite de Agua (L): ");
    scanf("%f", &limiteAgua);
    printf("Informe o limite de Energia (kWh): ");
    scanf("%f", &limiteEnergia);

    mochila(aparelhos, numAparelhos, limiteAgua, limiteEnergia);

    return 0;
}
