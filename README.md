UNIVERSIDADE FEDERAL DO MARANHÃO
BACHARELADO INTERDISCIPLINAR EM CIÊNCIA E TECNOLOGIA
ALUNA: JEANE SILVA GALVÃO MATRICULA: 20230101905

#include <stdio.h>
#include <string.h>

#define TOTAL_NOMES 50
#define TAM_NOME 30

char cadastro[TOTAL_NOMES][TAM_NOME];

int procurarNome(char texto[]) {
    int i;

    for(i = 0; i < TOTAL_NOMES; i++) {
        if(strcmp(cadastro[i], texto) == 0) {
            return i;
        }
    }

    return -1;
}

int main() {
    int opcao, i, posicao;
    char nome[TAM_NOME];
    char novoNome[TAM_NOME];

    do {
        printf("\n===== MENU =====\n");
        printf("1 - Adicionar nome\n");
        printf("2 - Pesquisar nome\n");
        printf("3 - Alterar nome\n");
        printf("4 - Excluir nome\n");
        printf("5 - Mostrar lista\n");
        printf("0 - Encerrar\n");
        printf("Opcao: ");
        scanf("%d", &opcao);

        getchar();

        switch(opcao) {

            case 1:
                printf("Digite um nome: ");
                fgets(nome, TAM_NOME, stdin);
                nome[strcspn(nome, "\n")] = '\0';

                if(procurarNome(nome) != -1) {
                    printf("Esse nome ja esta cadastrado!\n");
                    break;
                }

                posicao = -1;

                for(i = 0; i < TOTAL_NOMES; i++) {
                    if(cadastro[i][0] == '\0') {
                        posicao = i;
                        break;
                    }
                }

                if(posicao == -1) {
                    printf("Nao existe espaco disponivel.\n");
                } else {
                    strcpy(cadastro[posicao], nome);
                    printf("Cadastro realizado com sucesso!\n");
                }
                break;

            case 2:
                printf("Nome para pesquisa: ");
                fgets(nome, TAM_NOME, stdin);
                nome[strcspn(nome, "\n")] = '\0';

                posicao = procurarNome(nome);

                if(posicao == -1) {
                    printf("Nome nao localizado.\n");
                } else {
                    printf("Nome encontrado na posicao %d.\n", posicao);
                }
                break;

            case 3:
                printf("Qual nome deseja alterar? ");
                fgets(nome, TAM_NOME, stdin);
                nome[strcspn(nome, "\n")] = '\0';

                posicao = procurarNome(nome);

                if(posicao == -1) {
                    printf("Nome nao encontrado.\n");
                } else {

                    printf("Digite o novo nome: ");
                    fgets(novoNome, TAM_NOME, stdin);
                    novoNome[strcspn(novoNome, "\n")] = '\0';

                    if(procurarNome(novoNome) != -1) {
                        printf("Ja existe um registro com esse nome.\n");
                    } else {
                        strcpy(cadastro[posicao], novoNome);
                        printf("Alteracao concluida.\n");
                    }
                }
                break;

            case 4:
                printf("Informe o nome para exclusao: ");
                fgets(nome, TAM_NOME, stdin);
                nome[strcspn(nome, "\n")] = '\0';

                posicao = procurarNome(nome);

                if(posicao == -1) {
                    printf("Nome nao encontrado.\n");
                } else {
                    cadastro[posicao][0] = '\0';
                    printf("Registro removido.\n");
                }
                break;

            case 5:
                printf("\n--- NOMES CADASTRADOS ---\n");

                for(i = 0; i < TOTAL_NOMES; i++) {
                    if(cadastro[i][0] != '\0') {
                        printf("Indice %d: %s\n", i, cadastro[i]);
                    }
                }
                break;

            case 0:
                printf("Programa encerrado.\n");
                break;

            default:
                printf("Opcao invalida!\n");
        }

    } while(opcao != 0);

    return 0;
}
