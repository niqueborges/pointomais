# PontoMais — Setup inicial do projeto

## 1. Objetivo

Este documento registra, passo a passo, a criação da estrutura inicial do projeto PontoMais, incluindo o repositório Git local, a publicação no GitHub e a configuração inicial do GitHub Actions.

A documentação registra não apenas os comandos utilizados, mas também o motivo de cada etapa, os resultados esperados e os problemas encontrados durante a configuração.

## 2. Contexto do projeto

O PontoMais é uma plataforma fictícia de fidelidade criada para estudar uma arquitetura baseada em microsserviços.

O projeto será desenvolvido utilizando:

- Java 21
- Spring Boot
- React + TypeScript
- PostgreSQL
- APIs REST
- GitHub Actions
- Docker
- testes automatizados
- JaCoCo
- OpenAPI

Uma das regras de qualidade do projeto será manter cobertura mínima de **90% nos testes automatizados do backend**.

A implementação dos serviços será realizada gradualmente.

## 3. Estrutura inicial

A estrutura planejada inicialmente é:

```text
pointomais/
├── .github/
│   └── workflows/
│       └── ci.yml
├── customer-service/
├── points-service/
├── redemption-service/
├── api-gateway/
├── frontend/
├── docs/
├── .gitignore
└── README.md
```

O `docker-compose.yml` foi introduzido posteriormente, quando o `customer-service` passou a depender de PostgreSQL.

Neste primeiro momento, os diretórios dos serviços ainda não possuem código de aplicação.

## 4. Criação do projeto local

O diretório inicial foi criado com:

```bash
mkdir pointomais
cd pointomais
```

O comando `mkdir` cria o diretório do projeto e `cd` entra nesse diretório.

## 5. Inicialização do Git

O repositório Git foi inicializado com:

```bash
git init
```

Em seguida, a branch principal foi definida como `main`:

```bash
git branch -M main
```

A partir desse momento, o diretório passou a ser um repositório Git local.

## 6. Criação da estrutura de diretórios

Foram criados os diretórios planejados:

```bash
mkdir -p .github/workflows
mkdir -p customer-service
mkdir -p points-service
mkdir -p redemption-service
mkdir -p api-gateway
mkdir -p frontend
mkdir -p docs
```

O diretório `.github/workflows` será utilizado para armazenar os workflows do GitHub Actions.

## 7. README inicial

Foi criado o arquivo:

```bash
touch README.md
```

O README inicial descreve:

- objetivo do projeto;
- tecnologias previstas;
- arquitetura inicial;
- microsserviços planejados;
- requisito de cobertura mínima de 90%;
- CI/CD;
- roadmap.

O README não descreve funcionalidades como concluídas quando elas ainda não foram implementadas.

## 8. `.gitignore`

Foi criado o arquivo:

```bash
touch .gitignore
```

O `.gitignore` contém exclusões para arquivos e diretórios gerados durante o desenvolvimento, incluindo:

- `target/`
- `node_modules/`
- `dist/`
- arquivos `.env`
- diretórios de IDE;
- logs;
- arquivos de cobertura;
- arquivos temporários.

O objetivo é evitar que artefatos locais ou informações sensíveis sejam adicionados ao repositório.

## 9. Primeiro workflow de CI

Foi criado:

```text
.github/workflows/ci.yml
```

O primeiro workflow possui uma função deliberadamente simples: validar se os principais componentes da estrutura inicial existem.

O workflow executa:

```text
Checkout
    ↓
Verificação do README
    ↓
Verificação do .gitignore
    ↓
Verificação dos diretórios principais
```

Nesta etapa ainda não existe código Java ou React para compilar ou testar.

O CI será ampliado posteriormente para executar compilação, testes e verificação de cobertura.

## 10. Primeiro commit

Antes do primeiro commit foi utilizado:

```bash
git status
```

O resultado mostrou os arquivos ainda não rastreados.

Os arquivos foram adicionados:

```bash
git add .
```

O primeiro commit foi criado com:

```bash
git commit -m "chore: initialize project"
```

Commit criado:

```text
13e8fe4 chore: initialize project
```

Após o commit:

```bash
git status
```

retornou:

```text
nothing to commit, working tree clean
```

## 11. Instalação do GitHub CLI

O GitHub CLI (`gh`) não estava instalado inicialmente.

O sistema indicou as opções disponíveis. Foi utilizada a instalação via APT:

```bash
sudo apt update
sudo apt install gh
```

A instalação foi confirmada com:

```bash
gh --version
```

Versão utilizada:

```text
gh version 2.46.0
```

## 12. Autenticação no GitHub

A autenticação foi iniciada com:

```bash
gh auth login
```

Foram selecionadas as seguintes opções:

```text
GitHub.com
HTTPS
Authenticate Git with your GitHub credentials: Yes
Login with a web browser
```

O navegador não pôde ser aberto automaticamente a partir do WSL porque ferramentas como `xdg-open`, `wslview` e equivalentes não estavam disponíveis no ambiente.

O fluxo de autenticação foi concluído manualmente.

A autenticação foi verificada com:

```bash
gh auth status
```

O GitHub CLI confirmou a conta autenticada e o protocolo HTTPS.

### Observação de segurança

Códigos temporários, tokens e outras credenciais utilizados durante a autenticação não fazem parte desta documentação e não devem ser adicionados ao repositório.

## 13. Criação do repositório remoto

Com o repositório local já contendo o primeiro commit, o repositório GitHub foi criado utilizando:

```bash
gh repo create pointomais --public --source=. --remote=origin --push
```

O comando:

1. criou o repositório remoto;
2. adicionou o remoto `origin`;
3. enviou a branch `main`.

O repositório remoto passou a ser:

```text
niqueborges/pointomais
```

O remoto foi confirmado com:

```bash
git remote -v
```

Resultado esperado:

```text
origin  https://github.com/niqueborges/pointomais.git (fetch)
origin  https://github.com/niqueborges/pointomais.git (push)
```

## 14. Primeiro CI — falha

Após o primeiro `push`, o GitHub Actions executou o workflow.

A execução falhou.

O problema não estava relacionado ao GitHub, à autenticação ou ao código da aplicação.

A causa foi a estrutura de diretórios vazios.

O Git não versiona diretórios vazios. Portanto, embora os diretórios tivessem sido criados localmente, eles não existiam no repositório clonado pelo GitHub Actions.

O workflow continha verificações como:

```bash
test -d customer-service
```

Como `customer-service` não estava presente no repositório remoto, a verificação retornou código de saída `1`.

O job foi encerrado como:

```text
Process completed with exit code 1.
```

## 15. Correção com `.gitkeep`

Para preservar a estrutura inicial dos diretórios, foram criados arquivos `.gitkeep`:

```bash
touch customer-service/.gitkeep
touch points-service/.gitkeep
touch redemption-service/.gitkeep
touch api-gateway/.gitkeep
touch frontend/.gitkeep
touch docs/.gitkeep
```

Esses arquivos permitem que diretórios que ainda não possuem código sejam representados no Git.

Os arquivos foram adicionados:

```bash
git add .
```

E foi criado o segundo commit:

```bash
git commit -m "chore: add project structure"
```

O commit foi enviado ao GitHub:

```bash
git push
```

## 16. Segundo CI — sucesso

A nova execução foi consultada com:

```bash
gh run list
```

A execução correspondente ao segundo commit foi:

```text
38594135274
```

Os detalhes foram consultados com:

```bash
gh run view 38594135274
```

Resultado:

```text
✓ main CI
✓ repository-check
```

O primeiro workflow de CI passou com sucesso.

## 17. Warnings apresentados pelo GitHub Actions

A execução apresentou dois avisos que não impediram o sucesso do workflow.

### Node.js 20

O GitHub informou que `actions/checkout@v4` possui uma ação direcionada ao Node.js 20 e que a infraestrutura atual está executando essa ação sob Node.js 24.

Esse aviso não causou falha no workflow.

### Ubuntu

O GitHub também informou que o label:

```text
ubuntu-latest
```

será migrado para Ubuntu 26 a partir de 19 de outubro de 2026.

Esse aviso também não causou falha no workflow.

Esses avisos serão reavaliados quando o pipeline for ampliado.

## 18. Implementação inicial do customer-service

A segunda etapa de desenvolvimento começou com a geração do `customer-service` através do Spring Initializr.

### 18.1 Spring Boot

A primeira tentativa utilizou a versão `3.5.6`, mas o Spring Initializr retornou erro informando que a faixa de compatibilidade disponível exigia Spring Boot `4.0.0` ou superior.

A versão padrão informada pelo metadata do Initializr foi `4.1.1.RELEASE`. Entretanto, a versão publicada no Maven Central corresponde a `4.1.1`.

O `pom.xml` foi ajustado para:

```xml
<version>4.1.1</version>
```

O projeto foi configurado com:

- Java 21;
- Spring Boot 4.1.1;
- Spring Web MVC;
- Spring Data JPA;
- Bean Validation;
- PostgreSQL;
- dependências de teste geradas pelo Spring Boot.

### 18.2 Primeiro teste — falha de datasource

Após a geração do projeto, o primeiro:

```bash
./mvnw test
```

falhou durante a inicialização do contexto Spring.

A causa foi a ausência de configuração do datasource. O projeto possuía JPA e o driver PostgreSQL, mas ainda não informava ao Spring Boot qual banco deveria ser utilizado.

A decisão foi não introduzir H2 apenas para fazer o teste passar. Como PostgreSQL já faz parte da arquitetura definida, o ambiente deveria ser configurado com PostgreSQL real.

### 18.3 PostgreSQL com Docker

Foi criado o `docker-compose.yml` na raiz do projeto.

O primeiro serviço de infraestrutura é:

```text
customer-db
```

utilizando:

```text
postgres:18
```

Configuração inicial:

```text
Banco:     customer_db
Usuário:   pointomais
Porta:     5432
```

Os dados são persistidos no volume:

```text
pointomais_customer-db-data
```

O banco foi iniciado com:

```bash
docker compose up -d customer-db
```

A execução foi validada com:

```bash
docker compose ps
```

e:

```bash
docker compose exec customer-db pg_isready -U pointomais -d customer_db
```

Resultado:

```text
/var/run/postgresql:5432 - accepting connections
```

Os logs também confirmaram:

```text
database system is ready to accept connections
```

### 18.4 Configuração do datasource

O `customer-service` passou a utilizar:

```properties
spring.datasource.url=${DB_URL:jdbc:postgresql://localhost:5432/customer_db}
spring.datasource.username=${DB_USERNAME:pointomais}
spring.datasource.password=${DB_PASSWORD:pointomais_dev}
```

As variáveis de ambiente permitem substituir os valores padrão de desenvolvimento sem alterar o código versionado.
Os valores padrão (`localhost`, `pointomais` e `pointomais_dev`) são destinados exclusivamente ao ambiente local de desenvolvimento. Em outros ambientes, as credenciais devem ser fornecidas por configuração externa, sem serem incorporadas ao código.

Também foi configurado:

```properties
spring.jpa.hibernate.ddl-auto=update
spring.jpa.open-in-view=false
```

### 18.5 Segundo teste — sucesso

Após a configuração do PostgreSQL, o comando:

```bash
./mvnw test
```

foi executado novamente.

Resultado:

```text
Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
BUILD SUCCESS
```

Isso confirmou a integração inicial entre Spring Boot, JPA, driver PostgreSQL e o PostgreSQL executado em Docker.

## 19. Estado atual

Neste ponto, o projeto possui:

```text
✓ Repositório Git local
✓ Branch main
✓ README
✓ .gitignore
✓ Estrutura inicial de diretórios
✓ GitHub remoto
✓ GitHub Actions
✓ CI inicial executando com sucesso
✓ customer-service criado
✓ Java 21
✓ Spring Boot 4.1.1
✓ Maven Wrapper
✓ Spring Data JPA
✓ Bean Validation
✓ PostgreSQL
✓ PostgreSQL executando em Docker
✓ Configuração do datasource
✓ Teste de contexto executando com sucesso
```

Ainda não foram implementados:

```text
□ entidade Customer
□ DTOs
□ repository
□ service
□ controller
□ validações de negócio
□ tratamento de exceções
□ suíte de testes do domínio
□ JaCoCo
□ regra de cobertura de 90%
□ points-service
□ redemption-service
□ api-gateway
□ frontend
□ comunicação entre serviços
□ autenticação
□ mensageria
□ observabilidade
```

## 20. Próxima etapa

A próxima etapa será implementar o domínio inicial do `customer-service`, começando pela entidade `Customer` e evoluindo gradualmente para:

- DTOs;
- repository;
- service;
- controller;
- validações;
- tratamento de exceções;
- testes unitários e de integração;
- JaCoCo;
- regra de cobertura mínima de 90%.

A cobertura mínima de 90% será incorporada ao processo de build desde o início.

O objetivo é evitar que a cobertura seja adicionada posteriormente como uma exigência artificial. Os testes serão desenvolvidos junto com as regras de negócio.
