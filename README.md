# Gerenciador de Tarefas — ToDo List

*Aplicação Spring Boot com Thymeleaf para gerenciamento de tarefas.*

---

## 1. Sobre o Projeto

Este projeto é uma aplicação web desenvolvida com Spring Boot e Thymeleaf para gerenciamento de tarefas pessoais. O sistema permite ao usuário criar, editar, excluir e acompanhar o status de suas tarefas por meio de uma interface web simples e responsiva.

A aplicação utiliza armazenamento em memória, sem necessidade de banco de dados externo, e oferece recursos de filtragem para visualização de todas as tarefas, somente as pendentes ou somente as concluídas.

---

## 2. Tecnologias Utilizadas

| Dependência | Versão | Finalidade |
|---|---|---|
| Java | 21 | Linguagem de programação principal |
| Spring Boot Parent | 4.0.3 | Gerenciamento de versões e configurações base |
| spring-boot-starter-web | 4.0.3 | Suporte a MVC e servidor web embarcado (Tomcat) |
| spring-boot-starter-thymeleaf | 4.0.3 | Template engine para renderização de páginas HTML |
| spring-boot-starter-validation | 4.0.3 | Validação de campos de entrada com Bean Validation |
| spring-boot-devtools | 4.0.3 | Ferramentas de desenvolvimento com hot reload |
| Maven | — | Gerenciamento de dependências e build |

---

## 3. Arquitetura da Aplicação

A aplicação segue o padrão de arquitetura em camadas MVC (Model-View-Controller), amplamente adotado em projetos Spring Boot.

### 3.1 Camada Model

A entidade Tarefa representa o modelo de dados do sistema. Por não utilizar banco de dados externo, ela é armazenada em memória por meio do repositório.

| Atributo | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| id | Long | Sim (gerado) | Identificador único gerado automaticamente |
| titulo | String | Sim | Título da tarefa |
| descricao | String | Não | Descrição detalhada da tarefa |
| status | Enum/String | Sim | Status da tarefa: Pendente ou Concluída |

### 3.2 Camada Repository

A classe TarefaRepository é responsável pelo armazenamento das tarefas em memória. Ela gerencia a coleção de tarefas durante a execução da aplicação, incluindo 3 tarefas de exemplo pré-cadastradas na inicialização.

### 3.3 Camada Service

A classe TarefaService concentra a lógica de negócio da aplicação. Ela intermedia a comunicação entre o controller e o repositório, aplicando as regras antes de qualquer operação. Os métodos disponibilizados são: listarTodas, listarPendentes, listarConcluidas, buscarPorId, salvar, excluir e alternarStatus.

### 3.4 Camada Controller

O TarefaController é anotado com @Controller e é responsável por servir as páginas HTML renderizadas pelo Thymeleaf. Ele utiliza o objeto Model para passar dados do backend para o frontend e o RedirectAttributes para exibir mensagens de sucesso e erro após operações.

---

## 4. Funcionalidades

- Criar, editar e excluir tarefas
- Alternar status entre Pendente e Concluída
- Filtrar tarefas por status: todas, pendentes ou concluídas
- Validação de formulários com mensagens de erro
- Mensagens flash de sucesso e erro após operações
- 3 tarefas de exemplo pré-cadastradas na inicialização
- Interface responsiva com CSS customizado

---

## 5. Endpoints da Aplicação

| URL | Método | Descrição |
|---|---|---|
| /tarefas | GET | Listar todas as tarefas |
| /tarefas?filtro=pendentes | GET | Listar somente tarefas pendentes |
| /tarefas?filtro=concluidas | GET | Listar somente tarefas concluídas |
| /tarefas/novo | GET | Formulário para nova tarefa |
| /tarefas/editar/{id} | GET | Formulário para editar tarefa existente |
| /tarefas/salvar | POST | Salvar tarefa (criar ou atualizar) |
| /tarefas/excluir/{id} | POST | Excluir tarefa pelo ID |
| /tarefas/status/{id} | GET | Alternar status da tarefa entre Pendente e Concluída |

---

## 6. Interface Web (Thymeleaf)

A interface web é composta por páginas HTML renderizadas pelo Thymeleaf, que permite vincular dados do backend Java diretamente ao HTML por meio de atributos especiais prefixados com `th:`.

### 6.1 Página de Listagem (/tarefas)

Página principal da aplicação. Exibe todas as tarefas cadastradas em formato de lista ou tabela, com opções para editar, excluir e alternar o status de cada tarefa. Contém também os filtros de visualização para exibir todas as tarefas, somente pendentes ou somente concluídas.

### 6.2 Formulário de Nova Tarefa (/tarefas/novo)

Página com formulário para criação de uma nova tarefa. Exibe mensagens de erro de validação caso os campos obrigatórios não sejam preenchidos corretamente.

### 6.3 Formulário de Edição (/tarefas/editar/{id})

Página com formulário pré-preenchido com os dados da tarefa selecionada. Permite alterar os campos e salvar as modificações.

---

## 7. Filtros de Visualização

A página de listagem oferece três opções de filtro acessíveis por meio de botões ou parâmetros de URL:

| Filtro | URL | Descrição |
|---|---|---|
| Todas | /tarefas | Exibe todas as tarefas cadastradas |
| Pendentes | /tarefas?filtro=pendentes | Exibe somente as tarefas com status Pendente |
| Concluídas | /tarefas?filtro=concluidas | Exibe somente as tarefas com status Concluída |

---

## 8. Como Executar o Projeto

### 8.1 Pré-requisitos

- Java 21 instalado
- Maven instalado (ou utilize o wrapper `./mvnw`)

### 8.2 Executando a Aplicação

```bash
# Usando Maven Wrapper
./mvnw spring-boot:run

# Ou usando Maven instalado
mvn spring-boot:run
```

A aplicação será iniciada na porta 8080. Acesse `http://localhost:8080/tarefas` no navegador.

---

## 9. Guia de Uso do Sistema

### 9.1 Criar uma Tarefa

1. Acesse `http://localhost:8080/tarefas` no navegador
2. Clique no botão para criar uma nova tarefa
3. Preencha o campo Título (obrigatório)
4. Preencha o campo Descrição (opcional)
5. Clique em Salvar

### 9.2 Editar uma Tarefa

1. Na listagem de tarefas, clique no botão Editar da tarefa desejada
2. O formulário será pré-preenchido com os dados atuais
3. Altere os campos desejados e clique em Salvar

### 9.3 Excluir uma Tarefa

1. Na listagem de tarefas, clique no botão Excluir da tarefa desejada
2. A tarefa será removida e uma mensagem de confirmação será exibida

### 9.4 Alternar Status de uma Tarefa

1. Na listagem de tarefas, clique no botão de status da tarefa desejada
2. O status alternará automaticamente entre Pendente e Concluída

### 9.5 Filtrar Tarefas

1. Na página de listagem, utilize os botões de filtro disponíveis
2. Selecione Todas, Pendentes ou Concluídas conforme desejado
3. A listagem será atualizada automaticamente exibindo apenas as tarefas do filtro selecionado

---

## 10. Estrutura do Projeto

```
src/main/java/com/biopark/tarefas/
    TarefasAppApplication.java      (Classe principal)
    controller/
        TarefaController.java       (Controlador MVC)
    service/
        TarefaService.java          (Regras de negócio)
    repository/
        TarefaRepository.java       (Armazenamento em memória)
    model/
        Tarefa.java                 (Entidade Tarefa)

src/main/resources/
    static/css/                     (Estilos CSS)
    templates/                      (Páginas HTML Thymeleaf)
    application.properties          (Configurações da aplicação)
```

---

*Projeto acadêmico desenvolvido com Spring Boot e Thymeleaf.*
