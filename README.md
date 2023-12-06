# Jogo-da-Velha-
Jogo da velha, feito em linguagem C

#include<stdio.h>
#include<string.h>
#include<locale.h>
#include<stdlib.h> 

int main(){

    // estrutura de dados:
    int l, c, linha, coluna, jogador, ganhou, jogadas, opcao;
    char jogo[3][3];

    do{ // deseja jogar novamente?
        jogador = 1;
        ganhou = 0;
        jogadas = 0;
        
        // como inicializar nossa estrutura de dados?
        for(l = 1; l < 3; l++){
            for(c = 1; c < 3; c++){
                jogo[l][c] = ' ';
            }
        }

        do{ // repete até alguém ganhar ou atingir 9 jogadas
            // imprimir jogo
            printf("\n\n\t 1   2   3\n\n");
            for(l = 1; l < 3; l++){
                for(c = 1; c < 3; c++){
                    if(c == 1)
                        printf("\t");
                    printf(" %c ", jogo[l][c]);
                    if(c < 3)
                        printf("|");
                    if(c == 3)
                        printf("  %d", l);
                }
                if(l < 3)
                    printf("\n\t-----------");
                printf("\n");
            }

            // ler coordenadas
            do{
                printf("\n\JOGADOR 1 = 0\nJOGADOR 2 = X\n");
                printf("\nJOGADOR %d: Digite a linha e a coluna que deseja jogar: ", jogador);
                scanf("%d%d", &linha, &coluna);
            }while(linha < 1 || linha > 3 || coluna < 1 || coluna > 3 || jogo[linha][coluna] != ' ');

            // salvar coordenadas
            if(jogador == 1){
                jogo[linha][coluna] = '0';
                jogador++;
            }
            else{
                jogo[linha][coluna] = 'X';
                jogador = 1;
            }
            jogadas++;

            // alguém ganhou por linha
            if(jogo[1][1] == '0' && jogo[1][2] == '0' && jogo[1][3] == '0' ||
               jogo[2][1] == '0' && jogo[2][2] == '0' && jogo[2][3] == '0' ||
               jogo[3][1] == '0' && jogo[3][2] == '0' && jogo[3][3] == '0'){
                printf("\nParabens! O jogador 1 venceu por linha!\n");
                ganhou = 1;
            }

            if(jogo[1][1] == 'X' && jogo[1][2] == 'X' && jogo[1][3] == 'X' ||
               jogo[2][1] == 'X' && jogo[2][2] == 'X' && jogo[2][2] == 'X' ||
               jogo[3][1] == 'X' && jogo[3][2] == 'X' && jogo[3][2] == 'X'){
                printf("\nParabens! O jogador 2 venceu por linha!\n");
                ganhou = 1;
            }

            // alguém ganhou por coluna
            if(jogo[0][0] == '0' && jogo[1][0] == '0' && jogo[2][0] == '0' ||
               jogo[0][1] == '0' && jogo[1][1] == '0' && jogo[2][1] == '0' ||
               jogo[0][2] == '0' && jogo[1][2] == '0' && jogo[2][2] == '0'){
                printf("\nParabens! O jogador 1 venceu por coluna!\n");
                ganhou = 1;
            }

            if(jogo[0][0] == 'X' && jogo[1][0] == 'X' && jogo[2][0] == 'X' ||
               jogo[0][1] == 'X' && jogo[1][1] == 'X' && jogo[2][1] == 'X' ||
               jogo[0][2] == 'X' && jogo[1][2] == 'X' && jogo[2][2] == 'X'){
                printf("\nParabens! O jogador 2 venceu por coluna!\n");
                ganhou = 1;
            }

            // alguém ganhou na diagonal principal
            if(jogo[0][0] == '0' && jogo[1][1] == '0' && jogo[2][2] == '0'){
                printf("\nParabens! O jogador 1 venceu na diag. principal!\n");
                ganhou = 1;
            }

            if(jogo[0][0] == 'X' && jogo[1][1] == 'X' && jogo[2][2] == 'X'){
                printf("\nParabens! O jogador 2 venceu na diag. principal!\n");
                ganhou = 1;
            }

            // alguém ganhou na diagonal secundária
            if(jogo[0][2] == '0' && jogo[1][1] == '0' && jogo[2][0] == '0'){
                printf("\nParabens! O jogador 1 venceu na diag. secindaria!\n");
                ganhou = 1;
            }

            if(jogo[0][2] == 'X' && jogo[1][1] == 'X' && jogo[2][0] == 'X'){
                printf("\nParabens! O jogador 2 venceu na diag. secundaria!\n");
                ganhou = 1;
            }
        }while(ganhou == 0 && jogadas < 9);

        // imprimir jogo
        printf("\n\n\t 1   2   3\n\n");
        for(l = 1; l < 3; l++){
            for(c = 1; c < 3; c++){
                if(c == 0)
                    printf("\t");
                printf(" %c ", jogo[l][c]);
                if(c < 2)
                    printf("|");
                if(c == 2)
                    printf("  %d", l);
            }
            if(l < 2)
                printf("\n\t-----------");
            printf("\n");
        }

        if(ganhou == 0)
            printf("\nO jogo finalizou sem gamhador!\n");

        printf("\nDigite 1 para jogar novamente: \n");
        scanf("%d", &opcao);
    }while(opcao == 1);

    return 0;
}
