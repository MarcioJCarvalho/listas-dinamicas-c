# Listas dinamicas em liguagem C


## Pilha
```c
#include <stdio.h>
#include <conio.h>
#include <stdlib.h>

typedef struct no{
    int dado;
    struct no *proximo;
}no;

typedef struct pilha{
    no *topo;
}pilha;


void pilha_init(pilha *p){
    p->topo = NULL;
}

int add(int dado, pilha *p){
    no *ponteiro = (no*)malloc(sizeof(no));
    if(ponteiro == NULL){
        printf("Erro de alocação. \n");
        return 0;
    } else {
        ponteiro->dado = dado;
        ponteiro->proximo = p->topo;
        p->topo = ponteiro;
        return 0;
    }
}

int pop(pilha *p){
    no* ponteiro = p->topo;
    int dado;
    if(ponteiro == NULL){
        printf("Pilha esta vazia!. \n");
        return 0;
    } else {
        p->topo = ponteiro->proximo; // atualiza o topo para o futuro topo
        ponteiro->proximo = NULL; // pega o topo que esta sendo removido e desliga ele da lista
        dado = ponteiro->dado; // salva o bkp do que esta desenpilhando
        free(ponteiro); // desaloca da memória
        return dado;
    }
}

void listar_pilha(pilha *p){
    no *ponteiro = p->topo; // inicializa o ponteiro pelo topo
    if(ponteiro == NULL){
        printf("Pilha esta vazia!. \n");
    } else {
        while(ponteiro != NULL){
            printf("%d ", ponteiro->dado);
            ponteiro = ponteiro->proximo;
        }
        printf("\n");
    }
}


void main()
{
    char opcao;
    int valor; 
    pilha *pl = (pilha*)malloc(sizeof(pilha)); 
    if(pl == NULL){
        printf("Erro de alocação da pilha. \n");
        exit(0);
    } else {
        pilha_init(pl);
    }
    
    // menu
	while (opcao!='S' && opcao!='s')
	{
	  printf("[I]ncluir [D]eletar [S]air\n");
	  scanf("%c ", &opcao);
	  if (opcao=='i' || opcao=='I')     
	  {
	    printf("Valor para incluir na pilha: \n"); 
	    scanf("%d ", &valor);
	    add(valor, pl);
	    listar_pilha(pl);
	  } 
	  else if (opcao=='d' || opcao=='D')
	  {
  		pop(pl);
  		listar_pilha(pl);
	  }
	  else if (opcao=='s' || opcao=='S')
	  {
	    printf("Finalizando...");  
      } else {
          printf("Opção inválida!. \n");
      }
     
	}
	system ("clear");//limpa tela
	return;
}
```
