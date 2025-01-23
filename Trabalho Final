#include <stdio.h>
#include <string.h>
#include <stdlib.h>

#define MAX 100

typedef struct {
    char nome[100];
    char email[100];
    char senha[100];
    int tipo;  // 1 para admin, 2 para usuário comum
    int id; 
} Usuario;

typedef struct {
    char nome[100];
    int id;
} Filme;

typedef struct {
    Filme data[100];
    int inicio, fim;
} FilaF;

FilaF p; // Variável global
typedef struct {
    Usuario data[MAX];
    int inicio, fim;
} Fila;
Fila q; 

// Inicializa a fila
void initializeQueue(Fila *q) {
    q->inicio = q->fim = -1;
}

void inicializarFila(FilaF *p) {
    p->inicio = 0;
    p->fim = 0;
}

// Verifica se a fila está vazia
int isEmpty(Fila *q) {
    return q->inicio == -1;
}

// Verifica se a fila está cheia
int isFull(Fila *q) {
    return q->fim == MAX - 1;
}

// email já existe
int emailJaCadastrado(Fila *q, char *email) {
    for (int i = q->inicio; i <= q->fim; i++) {
        if (strcmp(q->data[i].email, email) == 0) {
            return 1;  // Email já cadastrado
        }
    }
    return 0;  // Email não encontrado
}

// cadastrar 
void cadastrar(Fila *q) {
    Usuario usuario;
    printf("Digite o nome: ");
    scanf(" %[^\n]%*c", usuario.nome);  // Para ler espaços
    printf("Digite o email: ");
    scanf("%s", usuario.email);

    // verifica se o email já foi cadastrado
    if (emailJaCadastrado(q, usuario.email)) {
        printf("Este email já está cadastrado. Tente outro.\n");
        return;
    }

    printf("Digite a senha: ");
    scanf("%s", usuario.senha);
    usuario.tipo = 2;  // Todos os usuários cadastrados serão tipo 2
    usuario.id = q->fim + 1;
    if (isFull(q)) {
        printf("Fila cheia! Não é possível adicionar mais usuários.\n");
    } else {
        if (isEmpty(q)) {
            q->inicio = q->fim = 0;
        } else {
            q->fim++;
        }
        q->data[q->fim] = usuario;
        printf("Usuário cadastrado com sucesso!\n");
    }
}

//  login
int Login(Fila *q, char *email, char *senha) {
    if (isEmpty(q)) {
        printf("Nenhum usuário cadastrado.\n");
        return 0;
    }
    for (int i = q->inicio; i <= q->fim; i++) {
        if (strcmp(q->data[i].email, email) == 0 && strcmp(q->data[i].senha, senha) == 0) {
            printf("Login bem-sucedido!\n");
            // Redireciona para a área apropriada de acordo com o tipo de usuário
            return i; // Retorna o índice do usuário logado para usar em suas opções
        }
    }
    printf("Login falhou. Usuário ou senha incorretos.\n");
    return -1;
}

//  inicializar o sistema com o administrador
void inicializarAdministrador(Fila *q) {
    Usuario administrador = {"Sr. Administrador", "adm@gmail.com", "123", 1, 0};  // Tipo 1 para admin
    q->inicio = q->fim = 0;
    q->data[q->fim] = administrador;
}

// função para verificar se filme já está cadastrado
int filmeJaCadastrado(FilaF *p, char *nome) {
    for (int i = 0; i < p->fim; i++) {
        if (strcmp(p->data[i].nome, nome) == 0) {
            return 1;
        }
    }
    return 0;
}

// função para listar usuários
void listarUsuario(Fila *q) {
    for (int i = 0; i <= q->fim; i++) {  // Exibe os usuários cadastrados
        printf("Nome: %s / ID: %d\n", q->data[i].nome, q->data[i].id);
    }
}

// função para excluir usuários
void excluirUsuario(Fila *q) {
    printf("Usuários:\n");
    for (int i = 1; i <= q->fim; i++) {  // Exibe os usuários cadastrados
        printf("Usuário: %s / ID: %d\n", q->data[i].nome, q->data[i].id);
    }

    int idUsuario;
    printf("Digite o id do usuário que deseja excluir: ");
    scanf("%d", &idUsuario);

    // Verifica se o ID informado é válido
    int encontrado = 0;
    for (int i = 1; i <= q->fim; i++) {
        if (q->data[i].id == idUsuario) {
            encontrado = 1;

            // Desloca todos os filmes após o filme excluído
            for (int j = i; j < q->fim - 1; j++) {
                q->data[j] = q->data[j + 1];
            }

            // Atualiza q->fim
            q->fim--;
            printf("Usuário excluído com sucesso!\n");
            break;
        }
    }

    if (!encontrado) {
        printf("Usuário com ID %d não encontrado!\n", idUsuario);
    }
}

// função para cadastrar filme
void cadastrarFilme(FilaF *p) {
    if (p->fim < 100) {
        Filme novoFilme;
        printf("Digite o nome do filme: ");
        getchar();
        fgets(novoFilme.nome, 100, stdin);
        novoFilme.nome[strcspn(novoFilme.nome, "\n")] = '\0';

        if (filmeJaCadastrado(p, novoFilme.nome)) {
            printf("Filme já cadastrado!\n");
            return;
        }

        novoFilme.id = p->fim + 1;
        p->data[p->fim] = novoFilme;
        p->fim++;

        printf("Filme cadastrado com sucesso! ID: %d\n", novoFilme.id);
    } else {
        printf("Fila cheia! Não é possível cadastrar mais filmes.\n");
    }
}

// função para editar filmes
void editarFilme(FilaF *p) {
    printf("Filmes:\n");
    for (int i = 0; i < p->fim; i++) {  // Exibe os filmes cadastrados
        printf("Filme: %s / ID: %d\n", p->data[i].nome, p->data[i].id);
    }

    int idFilme;
    printf("Digite o id do filme que deseja editar: ");
    scanf("%d", &idFilme);

    // Verifica se o ID informado é válido
    int encontrado = 0;
    for (int i = 0; i < p->fim; i++) {
        if (p->data[i].id == idFilme) {
            encontrado = 1;

            // Editar o filme
            printf("Editar nome do filme (atualmente: %s): ", p->data[i].nome);
            getchar();  // Limpa o buffer do teclado
            fgets(p->data[i].nome, 100, stdin);
            p->data[i].nome[strcspn(p->data[i].nome, "\n")] = '\0';  // Remove a nova linha

            printf("Filme editado com sucesso!\n");
            break;
        }
    }

    if (!encontrado) {
        printf("Filme com ID %d não encontrado!\n", idFilme);
    }
}

// função para excluir filmes
void excluirFilme(FilaF *p) {
    printf("Filmes:\n");
    for (int i = 0; i < p->fim; i++) {  // Exibe os filmes cadastrados
        printf("Filme: %s / ID: %d\n", p->data[i].nome, p->data[i].id);
    }

    int idFilme;
    printf("Digite o id do filme que deseja excluir: ");
    scanf("%d", &idFilme);

    // Verifica se o ID informado é válido
    int encontrado = 0;
    for (int i = 0; i < p->fim; i++) {
        if (p->data[i].id == idFilme) {
            encontrado = 1;

            // Desloca todos os filmes após o filme excluído
            for (int j = i; j < p->fim - 1; j++) {
                p->data[j] = p->data[j + 1];
            }

            // Atualiza p->fim
            p->fim--;
            printf("Filme excluído com sucesso!\n");
            break;
        }
    }

    if (!encontrado) {
        printf("Filme com ID %d não encontrado!\n", idFilme);
    }
}


// função para buscar filme por título
void buscarFilmePorTitulo(FilaF *p, char *titulo) {
    int encontrado = 0;
    for (int i = 0; i < p->fim; i++) {
        if (strstr(p->data[i].nome, titulo) != NULL) {
            printf("Filme encontrado: %s / ID: %d\n", p->data[i].nome, p->data[i].id);
            encontrado = 1;
        }
    }
    if (!encontrado) {
        printf("Nenhum filme encontrado com o titulo: %s\n", titulo);
    }
}

// função para a área Administrativa
void areaAdministrativa() {
    int opcaoAdm;
    char titulo[100];
    do {
        printf("\nOpções da Área Administrativa:\n");
        printf("1. Cadastrar filme\n");
        printf("2. Editar filme\n");
        printf("3. Excluir filme\n");
        printf("4. Buscar filme por título\n");
        printf("5. Listar usuários\n");
        printf("6. Excluir usuários\n");
        printf("7. Deslogar\n");
        printf("Escolha uma opção: ");
        scanf("%d", &opcaoAdm);

        switch (opcaoAdm) {
            case 1:
                printf("Cadastrar filme\n");
                cadastrarFilme(&p);
                break;
            case 2:
                printf("Editar filme\n");
                editarFilme(&p);
                break;
            case 3:
                printf("Excluir filme\n");
                excluirFilme(&p);
                break;
            case 4:
                printf("Digite o título do filme que deseja buscar: ");
                getchar();  // Limpa o buffer do teclado
                fgets(titulo, 100, stdin);
                titulo[strcspn(titulo, "\n")] = '\0';  // Remove a nova linha
                buscarFilmePorTitulo(&p, titulo);
                break;
            case 5:
                printf("Listar usuários\n");
                listarUsuario(&q);
                break;
            case 6:
                printf("Excluir Usuários\n");
                excluirUsuario(&q);
                break;
            case 7:
                printf("Deslogando...\n");
                break;
            default:
                printf("Opção inválida!\n");
        }
    } while (opcaoAdm != 7);  // Continua até o usuário escolher deslogar
}

// função para a área do Usuário Comum
void areaUsuario() {
    int opcaoUsuario;
    char titulo[100];
    do {
        printf("\nOpções para Usuário:\n");
        printf("1. Listar filmes\n");
        printf("2. Buscar filme por título\n");
        printf("3. Deslogar\n");
        printf("Escolha uma opção: ");
        scanf("%d", &opcaoUsuario);

        switch (opcaoUsuario) {
            case 1:
                printf("Listar filmes\n");
                // função para listar filmes vai aqui
                break;
            case 2:
                printf("Digite o título do filme que deseja buscar: ");
                getchar();  // Limpa o buffer do teclado
                fgets(titulo, 100, stdin);
                titulo[strcspn(titulo, "\n")] = '\0';  // Remove a nova linha
                buscarFilmePorTitulo(&p, titulo);
                break;
            case 3:
                printf("Deslogando...\n");
                break;
            default:
                printf("Opção inválida!\n");
        }
    } while (opcaoUsuario != 3);  // Continua até o usuário escolher deslogar
}

int main() {
    initializeQueue(&q);
    inicializarFila(&p);
    inicializarAdministrador(&q);  // Inicializa o administrador
    int opcao;
    char email[100], senha[100];
    int usuarioLogado = -1;

    do {
        printf("\n1. Cadastrar\n2. Fazer Login\n3. Sair\nEscolha: ");
        scanf("%d", &opcao);
        switch (opcao) {
            case 1:
                cadastrar(&q);
                break;
            case 2:
                printf("Digite o email: ");
                scanf("%s", email);
                printf("Digite a senha: ");
                scanf("%s", senha);
                usuarioLogado = Login(&q, email, senha);
                if (usuarioLogado != -1) {
                    if (q.data[usuarioLogado].tipo == 1) {
                        areaAdministrativa();
                    } else {
                        areaUsuario();
                    }
                }
                break;
            case 3:
                printf("Encerrando o sistema...\n");
                break;
            default:
                printf("Opção inválida!\n");
        }
    } while (opcao != 3);

    return 0;
}
