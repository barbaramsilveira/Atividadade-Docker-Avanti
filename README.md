# ms-saudacoes-aleatorias
Microsserviço de venda de saudações aleatórias escrito em Go (Golang), desenvolvido pelos instrutores do Bootcamp DevOps da Escola Atlântico Avanti como base para os desafios práticos do curso.
Minha contribuição neste repositório foi a execução dos Dockerfiles de cada serviço da aplicação e a criação do arquivo do Docker Compose para orquestrar todos os containers localmente.

# Contexto
O código da aplicação foi fornecido pelos instrutores. O desafio consistia em containerizar os três serviços que compõem a aplicação e integrá-los por meio de um docker-compose.yml, simulando um ambiente próximo ao de produção.

---

## ⚙️ Pipeline CI/CD

A pipeline é disparada automaticamente a cada `push` ou `pull request` na branch `main` e executa as seguintes etapas:

| Etapa | Job | Descrição |
|-------|-----|-----------|
| Lint | `build-lint` | Verifica a qualidade e formatação do código Go |
| Testes | `test` | Executa os testes automatizados da aplicação |
| Build & Push | `release` | Constrói a imagem Docker e publica no Docker Hub |
| Deploy | `deploy` | Realiza o deploy da imagem no Koyeb via Terraform |
| Cleanup | `cleanup` | Destrói a infraestrutura no Koyeb *(aprovação manual)* |

> O job de **cleanup** requer aprovação manual antes de executar, evitando destruição acidental do ambiente.

---

## Variáveis de Ambiente (Secrets)

Configure as seguintes variáveis em **Settings → Secrets and variables → Actions** do seu repositório:

| Variável | Descrição |
|----------|-----------|
| `DOCKER_USER` | Seu usuário do Docker Hub |
| `DOCKER_PASS` | Sua senha ou token do Docker Hub |
| `KOYEB_TOKEN` | Token de API do Koyeb para o deploy |

---

## Como Usar

### 1. Clone o repositório

```bash
git clone https://github.com/<seu-usuario>/ms-saudacoes-aleatorias.git
cd ms-saudacoes-aleatorias
```

### 2. Configure os secrets

Acesse **Settings → Secrets → Actions** e adicione `DOCKER_USER`, `DOCKER_PASS` e `KOYEB_TOKEN`.

### 3. Faça um push e acompanhe a pipeline

```bash
git add .
git commit -m "feat: minha alteração"
git push origin main
```

Acompanhe a execução em: **Actions** → `CI/CD Pipeline`

---

## Rodando Localmente

**Pré-requisitos:** Go 1.21+, Docker

```bash
# Executar a aplicação
go run main.go

# Rodar os testes
go test ./...

# Build da imagem Docker
docker build -t ms-saudacoes-aleatorias .

# Rodar o container
docker run -p 8080:8080 ms-saudacoes-aleatorias
```

---

## ☁️ Deploy — Koyeb

O deploy é feito automaticamente via **Terraform** no [Koyeb](https://www.koyeb.com/), disparado após o push da imagem no Docker Hub.

Para destruir a infraestrutura, acesse a pipeline no GitHub Actions, vá até o job **cleanup** e aprove a execução manual.

---

## 🛠️ Tecnologias

![Go](https://img.shields.io/badge/Go-1.21+-00ADD8?style=flat&logo=go&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Hub-2496ED?style=flat&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-CI%2FCD-2088FF?style=flat&logo=github-actions&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-IaC-7B42BC?style=flat&logo=terraform&logoColor=white)
![Koyeb](https://img.shields.io/badge/Koyeb-Deploy-121212?style=flat&logo=koyeb&logoColor=white)

---

## Referências

- [Documentação Go](https://go.dev/doc/)
- [GitHub Actions Docs](https://docs.github.com/en/actions)
- [Docker Hub](https://hub.docker.com/)
- [Koyeb Docs](https://www.koyeb.com/docs)
- [Terraform Docs](https://developer.hashicorp.com/terraform/docs)

---

> Desenvolvido como parte do desafio de **Pipeline de CI/CD** — Avanti DVP 🚀
