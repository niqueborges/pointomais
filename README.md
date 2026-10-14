# PontoMais

Plataforma de fidelidade desenvolvida para estudo prático de arquitetura de microsserviços, desenvolvimento backend com Java e Spring Boot e frontend com React.

O projeto simula uma plataforma de benefícios na qual clientes acumulam pontos através de transações e podem utilizá-los para realizar resgates.

## Objetivo

O PontoMais foi criado como projeto prático para estudar e aplicar conceitos utilizados no desenvolvimento de aplicações distribuídas:

- Java 21
- Spring Boot
- Arquitetura de microsserviços
- APIs REST
- React + TypeScript
- PostgreSQL
- Testes automatizados
- CI/CD
- Docker
- OpenAPI
- Segurança de APIs
- Observabilidade

## Arquitetura planejada

A aplicação será composta inicialmente pelos seguintes componentes:

- `customer-service` — gerenciamento de clientes
- `points-service` — gerenciamento de pontos e movimentações
- `redemption-service` — gerenciamento de resgates
- `api-gateway` — ponto de entrada das APIs
- `frontend` — aplicação web React

Cada microsserviço deverá possuir responsabilidade própria e não deverá acessar diretamente o banco de dados pertencente a outro serviço.

A arquitetura será construída progressivamente. Nem todos os componentes listados estão implementados ainda.

## Qualidade e testes

O projeto possui como requisito uma cobertura mínima de **90% nos testes automatizados do backend**.

A cobertura será acompanhada através do JaCoCo e integrada ao processo de build.

O objetivo não é apenas atingir um percentual de cobertura, mas testar efetivamente:

- regras de negócio;
- cenários de sucesso;
- cenários de erro;
- validações;
- exceções;
- integrações entre componentes.

A exigência de 90% será incorporada ao processo de CI para impedir que alterações sejam integradas quando a cobertura estiver abaixo do limite definido.

## CI/CD

O projeto utiliza GitHub Actions para automatizar as validações do repositório.

A primeira etapa do CI já foi implementada e validada.

Atualmente, o pipeline verifica:

- existência do README;
- existência do `.gitignore`;
- existência da estrutura inicial do projeto.

O pipeline será ampliado conforme os componentes da aplicação forem implementados.

A evolução planejada é:

```text
Estrutura do projeto
        ↓
Compilação
        ↓
Testes
        ↓
Cobertura JaCoCo
        ↓
Verificação dos 90%
        ↓
Build da aplicação
        ↓
Docker
        ↓
Etapas adicionais de CI/CD
```

## Status atual

### Etapa 1 — Fundação do projeto

**Concluída**

- [x] Criar repositório Git local
- [x] Definir `main` como branch principal
- [x] Criar estrutura inicial do monorepo
- [x] Criar README
- [x] Criar `.gitignore`
- [x] Configurar GitHub CLI
- [x] Criar repositório no GitHub
- [x] Configurar remoto `origin`
- [x] Criar primeiro workflow do GitHub Actions
- [x] Executar CI
- [x] Corrigir problema relacionado a diretórios vazios
- [x] Validar CI com sucesso
- [x] Documentar o processo inicial

### Etapa 2 — Customer Service

**Próxima etapa**

- [ ] Criar projeto Spring Boot
- [ ] Configurar Java 21
- [ ] Configurar Maven
- [ ] Configurar PostgreSQL
- [ ] Criar entidade `Customer`
- [ ] Criar DTOs
- [ ] Criar repository
- [ ] Criar service
- [ ] Criar controller
- [ ] Implementar validações
- [ ] Implementar tratamento de exceções
- [ ] Criar testes
- [ ] Configurar JaCoCo
- [ ] Exigir cobertura mínima de 90%
- [ ] Integrar testes ao CI

### Etapa 3 — Points Service

- [ ] Criar serviço de pontos
- [ ] Criar carteira de pontos
- [ ] Criar movimentações
- [ ] Implementar créditos
- [ ] Implementar débitos
- [ ] Criar testes
- [ ] Integrar ao CI

### Etapa 4 — Comunicação entre serviços

- [ ] Definir contratos entre serviços
- [ ] Implementar comunicação REST
- [ ] Tratar falhas de comunicação
- [ ] Implementar testes de integração

### Etapa 5 — Redemption Service

- [ ] Criar serviço de resgates
- [ ] Criar catálogo de benefícios
- [ ] Validar saldo
- [ ] Registrar resgates
- [ ] Implementar estados do resgate
- [ ] Criar testes
- [ ] Integrar ao CI

### Etapa 6 — API Gateway

- [ ] Criar API Gateway
- [ ] Configurar roteamento
- [ ] Centralizar entrada das APIs
- [ ] Configurar CORS
- [ ] Implementar tratamento de erros

### Etapa 7 — Frontend

- [ ] Criar aplicação React
- [ ] Configurar TypeScript
- [ ] Configurar Vite
- [ ] Implementar integração com API Gateway
- [ ] Criar tela do cliente
- [ ] Criar consulta de saldo
- [ ] Criar extrato
- [ ] Criar catálogo de benefícios
- [ ] Criar fluxo de resgate
- [ ] Implementar tratamento de erros

### Etapa 8 — Infraestrutura

- [ ] Docker
- [ ] Docker Compose
- [ ] Configuração por ambiente
- [ ] Health checks
- [ ] CI/CD ampliado

### Etapa 9 — Segurança

- [ ] Spring Security
- [ ] Autenticação
- [ ] JWT
- [ ] Autorização
- [ ] Proteção das APIs

### Etapa 10 — Observabilidade e evolução

- [ ] Logging estruturado
- [ ] Correlation ID
- [ ] Métricas
- [ ] Monitoramento
- [ ] OpenAPI
- [ ] Mensageria
- [ ] Avaliação de resiliência

## Documentação

O histórico de construção do projeto está sendo documentado em:

[`docs/setup.md`](docs/setup.md)

O objetivo é registrar os comandos utilizados, decisões tomadas, problemas encontrados e respectivas soluções.

A documentação será atualizada conforme o projeto evoluir.

## Estrutura atual

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
│   ├── setup.md
│   └── ...
├── .gitignore
├── README.md
└── docker-compose.yml
```

Os diretórios dos componentes ainda em desenvolvimento podem conter apenas `.gitkeep`.

## Histórico

### 2026-10-14

Fundação inicial do projeto concluída.

- Repositório Git criado.
- Repositório GitHub criado.
- GitHub Actions configurado.
- Primeiro CI executado.
- Falha inicial identificada e corrigida devido à ausência de diretórios vazios no Git.
- CI validado com sucesso.
- Processo documentado em `docs/setup.md`.

## Licença

Projeto desenvolvido para fins educacionais e de portfólio.