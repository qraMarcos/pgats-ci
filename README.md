# PGATS CI — Integração Contínua com GitLab CI e Playwright

Projeto desenvolvido para prática de Integração Contínua (CI) utilizando GitLab CI, Playwright e geração automatizada de relatórios com Allure Report.

O objetivo do projeto é automatizar a execução de testes E2E, gerar relatórios detalhados e disponibilizar os resultados automaticamente pela web utilizando GitLab Pages.

---

# Tecnologias utilizadas

- Node.js
- Playwright
- GitLab CI
- Allure Report
- GitLab Pages

---

# Exercícios Implementados

## Pipeline de Integração Contínua

Foi criada uma pipeline utilizando GitLab CI para automatizar a execução dos testes E2E do projeto.

A pipeline foi configurada para:

- Instalar dependências automaticamente
- Instalar os browsers do Playwright
- Executar os testes E2E
- Gerar artifacts da execução
- Gerar relatórios JUnit
- Executar automaticamente a cada push no repositório

Arquivo utilizado:

```yml
.gitlab-ci.yml
```

---

## Melhoria da Pipeline com Allure Report

Após a implementação inicial da pipeline, foi integrado o Allure Report para melhorar a visualização dos resultados dos testes dentro do mesmo fluxo de Integração Contínua.

Com isso, a pipeline passou a:

- Gerar relatórios visuais automatizados
- Exibir detalhes completos das execuções
- Manter histórico dos testes
- Publicar automaticamente os relatórios na web
- Permitir acesso aos resultados sem necessidade de download manual

---

## Fluxo final da pipeline

1. Instalação das dependências
2. Instalação dos browsers do Playwright
3. Execução dos testes automatizados
4. Geração do Allure Report
5. Criação dos artifacts
6. Publicação automática no GitLab Pages

---

# Relatório online

O relatório Allure pode ser acessado diretamente pelo navegador:

```txt
https://qramarcos.gitlab.io/pgats-ci
```

---

# Estrutura do projeto

```txt
.
├── e2e/
├── playwright-report/
├── allure-results/
├── allure-report/
├── package.json
├── playwright.config.ts
└── .gitlab-ci.yml
```

---

# Como executar o projeto localmente

## Instalar dependências

```bash
yarn
```

---

## Instalar browsers do Playwright

```bash
yarn playwright install --with-deps
```

---

## Executar testes

```bash
yarn e2e
```

---

# Gerar relatório Allure localmente

## Instalar Allure Commandline

```bash
npm install -g allure-commandline
```

---

## Gerar relatório

```bash
allure generate allure-results --clean -o allure-report
```

---

## Abrir relatório

```bash
allure open allure-report
```

---

# Funcionamento da Integração Contínua

A cada push realizado no GitLab:

1. A pipeline é iniciada automaticamente
2. Os testes Playwright são executados
3. O relatório Allure é gerado
4. O GitLab Pages publica automaticamente o resultado

---

# Autor

Projeto desenvolvido para prática de Integração Contínua e automação de testes E2E utilizando GitLab CI e Playwright.