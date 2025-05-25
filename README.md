1. Definições iniciais e estrutura dos dados

const int MAX_APARELHOS = 10;
const int MAX_NOME = 50;

typedef struct {

    char nome[MAX_NOME];
    float consumoEnergia;
    float consumoAgua;
    int prioridade;
} Aparelho;

Definimos um limite máximo de aparelhos que o programa pode armazenar (10) e tamanho máximo para o nome dos aparelhos.
A estrutura Aparelho para armazenar nome, consumo de energia e água, e a prioridade do aparelho.

Tabela de consumo estimado (função mostrarTabelaEstimativa)

void mostrarTabelaEstimativa() {

    printf("\nTabela de Consumo Estimado de Aparelhos:\n");
    printf("1. Geladeira: 15-20 kWh/mês\n");
    printf("2. Micro-ondas: 1-2 kWh/mês\n");
    printf("3. Chuveiro: 50-100 kWh/mês\n");
    printf("4. Máquina de Lavar: 10-30 kWh/mês\n");
    printf("5. Lava-louças: 10-20 kWh/mês\n\n");
}

Apresentamos ao usuário uma tabela de referência com estimativas comuns de consumo mensal para alguns aparelhos, serve para ajudar o usuário a informar dados mais precisos.

Função de seleção dos aparelhos (mochila)
{

 
 
 
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
    printf("Total utilizado: Água = %.1f L | Energia = %.1f kWh\n", aguaUsada, energiaUsada);
}
}
A função recebe a lista de aparelhos com seus consumos e prioridades, além dos limites mensais para água e energia. Ela percorre a lista na ordem em que os aparelhos foram inseridos, considerando que o usuário deve informar os aparelhos seguindo a prioridade desejada. Durante a iteração, seleciona os aparelhos enquanto a soma dos consumos de água e energia não ultrapassa os limites definidos. Por fim, exibe os aparelhos escolhidos e o total acumulado de consumo, indicando o que pode ser utilizado dentro dos limites estabelecidos.

Função principal (main)


 
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
        printf("Consumo de Água (L): ");
        scanf("%f", &aparelhos[i].consumoAgua);
        printf("Prioridade (1 - Muito Alta, 5 - Muito Baixa): ");
        scanf("%d", &aparelhos[i].prioridade);
    }

    printf("\nInforme o limite de Água (L): ");
    scanf("%f", &limiteAgua);
    printf("Informe o limite de Energia (kWh): ");
    scanf("%f", &limiteEnergia);

    mochila(aparelhos, numAparelhos, limiteAgua, limiteEnergia);

    return 0;
}

O programa começa mostrando ao usuário uma tabela com estimativas de consumo típicas de aparelhos domésticos para ajudar na hora de informar os dados. Em seguida, pergunta quantos aparelhos ele deseja cadastrar. Para cada aparelho, o programa solicita o nome, o consumo de água e energia, além da prioridade de uso. Depois, pergunta os limites mensais disponíveis para água e energia. Com esses dados, chama a função responsável por selecionar e mostrar quais aparelhos o usuário pode usar sem ultrapassar esses limites, considerando as prioridades informadas

Pseudocódigo


INÍCI0
 
 DEFINIR constante MAX_APARELHOS = 10
  DEFINIR constante MAX_NOME = 50

  DEFINIR estrutura Aparelho:
    nome: string[MAX_NOME]
    consumoEnergia: float
    consumoAgua: float
    prioridade: inteiro

  FUNÇÃO mostrarTabelaEstimativa:
    IMPRIMIR tabela com estimativas de consumo para aparelhos comuns

  FUNÇÃO mochila(aparelhos, n, limiteAgua, limiteEnergia):
    aguaUsada = 0
    energiaUsada = 0
    IMPRIMIR "Aparelhos Selecionados..."
    PARA i DE 0 ATÉ n-1 FAÇA
      SE (aguaUsada + aparelhos[i].consumoAgua <= limiteAgua) E (energiaUsada + aparelhos[i].consumoEnergia <= limiteEnergia) ENTÃO
        IMPRIMIR informações do aparelho
        aguaUsada += aparelhos[i].consumoAgua
        energiaUsada += aparelhos[i].consumoEnergia
      FIM SE
    FIM PARA
    IMPRIMIR totais usados

  INÍCIO PRINCIPAL
    CHAMAR mostrarTabelaEstimativa

   // LER numAparelhos

PARA i DE 0 ATÉ numAparelhos-1 FAÇA
     // LER nome do aparelho
      LER consumoEnergia do aparelho
      LER consumoAgua do aparelho
      LER prioridade do aparelho
      ARMAZENAR em aparelhos[i]
    FIM PARA

LER limiteAgua
    LER limiteEnergia

 CHAMAR mochila(aparelhos, numAparelhos, limiteAgua, limiteEnergia)

FIM}



Para verificar a eficácia do algoritmo, realizamos diversos testes simulando cenários variados de consumo e limites. Por exemplo, incluímos aparelhos com diferentes consumos e prioridades, e configuramos limites de água e energia para verificar a seleção resultante. Em todos os casos, o algoritmo selecionou corretamente os aparelhos de maior prioridade enquanto respeitou os limites estabelecidos, evitando ultrapassagens. Em um teste prático, ao cadastrar uma geladeira, um micro-ondas e um chuveiro com prioridades decrescentes, o algoritmo selecionou os dois primeiros aparelhos, pois a soma de seus consumos estava dentro do limite, e excluiu o terceiro para não exceder os recursos disponíveis. Isso demonstra que o algoritmo cumpre seu objetivo de forma eficaz.
