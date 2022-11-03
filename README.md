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

## Fila
```c
/******************************************************************************

                            Online C Compiler.
                Code, Compile, Run and Debug C program online.
Write your code in this editor and press "Run" button to compile and execute it.

*******************************************************************************/

#include <stdio.h>
#include <conio.h>
#include <stdlib.h>

typedef struct no{
    int dado;
    struct no *proximo;
}no;

typedef struct fila{
    no *inicio;
    no *fim 
}fila;


void fila_init(fila *f){
    f->inicio = NULL;
}

void enfileirar(int dado, fila *f){
    no *ponteiro = (no*)malloc(sizeof(no)); // alocamento do novo nó
    if(ponteiro == NULL){
        printf("Erro de alocação. \n");
        return;
    } else {
        ponteiro->dado = dado;
        ponteiro->proximo = NULL; // evita erros em tempo de execução
        // verifica de o inicio da fila é nulo
        if(f->inicio == NULL){
            f->inicio = ponteiro;
        } else {
            f-> fim->proximo = ponteiro;
        }
        
        f->fim = ponteiro; // para qualquer inserção na fila
        return;
    }
}

int desenfileira(fila *f){
    no *ponteiro = f->inicio;
    int dado;
    if(ponteiro != NULL){
        f->inicio = ponteiro->proximo;
        ponteiro->proximo = NULL;
        dado = ponteiro->dado;
        free(ponteiro); // desaloca memoria
        if(f->inicio == NULL){
            f->fim = NULL;
        }
        return dado;
    } else {
        printf("Fila esta vazia!. \n");
        return 0;
    }
}

void listar_fila(fila *f){
    no *ponteiro = f->inicio; // inicializa o ponteiro
    if(ponteiro != NULL){
        while(ponteiro != NULL){
            printf("%d ", ponteiro->dado);
            ponteiro = ponteiro->proximo;
        }
        printf("\n");
    } else {
        printf("Fila esta vazia!. \n");
        return;
    }
}


void main()
{
    char opcao;
    int valor; 
    fila *fl = (fila*)malloc(sizeof(fila)); 
    if(fl == NULL){
        printf("Erro de alocação da fila. \n");
        exit(0);
    } else {
        fila_init(fl);
    }
    
    // menu
	while (opcao!='S' && opcao!='s')
	{
	  printf("[I]ncluir [D]eletar [S]air\n");
	  scanf("%c ", &opcao);
	  if (opcao=='i' || opcao=='I')     
	  {
	    printf("Valor para incluir na fila: \n"); 
	    scanf("%d ", &valor);
	    enfileirar(valor, fl);
	    listar_fila(fl);
	  } 
	  else if (opcao=='d' || opcao=='D')
	  {
  		desenfileira(fl);
  		listar_fila(fl);
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
