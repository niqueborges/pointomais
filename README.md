# PontoMais

Plataforma de fidelidade desenvolvida para estudo de arquitetura de microsserviços, desenvolvimento backend com Java e Spring Boot e frontend com React.

O projeto simula uma plataforma de benefícios na qual clientes acumulam pontos através de transações e podem utilizá-los para realizar resgates.

## Objetivo

O PontoMais foi criado como projeto prático para estudar e aplicar:

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

## Arquitetura

A aplicação será composta inicialmente pelos seguintes componentes:

- `customer-service` — gerenciamento de clientes
- `points-service` — gerenciamento de pontos e movimentações
- `redemption-service` — gerenciamento de resgates
- `api-gateway` — ponto de entrada das APIs
- `frontend` — aplicação web React

Cada microsserviço deverá possuir responsabilidade própria e não deverá acessar diretamente o banco de dados pertencente a outro serviço.

## Requisito de qualidade

O projeto possui como requisito uma cobertura mínima de **90% nos testes automatizados do backend**.

A cobertura será acompanhada através do JaCoCo e integrada ao processo de build.

O objetivo não é apenas atingir um percentual de cobertura, mas testar efetivamente as regras de negócio, cenários de sucesso, erros e comportamentos de exceção.

## CI/CD

O projeto utilizará GitHub Actions para automatizar inicialmente:

1. compilação;
2. execução dos testes;
3. verificação da cobertura;
4. validações do projeto.

O pipeline será ampliado conforme novos componentes forem implementados.

## Status

Em desenvolvimento.

### Roadmap

- [ ] Estrutura inicial do monorepo
- [ ] `customer-service`
- [ ] Testes unitários
- [ ] Cobertura mínima de 90%
- [ ] PostgreSQL
- [ ] `points-service`
- [ ] Comunicação entre microsserviços
- [ ] `redemption-service`
- [ ] API Gateway
- [ ] Frontend React
- [ ] Docker Compose
- [ ] CI/CD completo
- [ ] Segurança com Spring Security/JWT
- [ ] Documentação OpenAPI
- [ ] Observabilidade
- [ ] Mensageria

## Licença

Projeto desenvolvido para fins educacionais e de portfólio.