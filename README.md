# PGATS-CI

Projeto desenvolvido para prática de Integração Contínua utilizando GitLab CI/CD, Playwright e Allure Reports.

---

# Exercício 1 — Pipeline de Integração Contínua no GitLab CI

## Objetivo

Implementar uma pipeline de Integração Contínua utilizando uma ferramenta diferente do GitHub Actions.

Ferramenta escolhida:

* entity["company","GitLab","GitLab DevOps Platform"] CI/CD

---

## Tecnologias utilizadas

* Node.js
* Yarn
* Playwright
* GitLab CI/CD
* Allure Report

---

## Estrutura do projeto

```bash
.
├── e2e/
│   └── example.spec.js
├── playwright.config.js
├── package.json
├── .gitlab-ci.yml
└── README.md
```

---

## Configuração da pipeline

Arquivo:

```bash
.gitlab-ci.yml
```

Pipeline criada:

```yml
image: node:24

stages:
  - test

cache:
  paths:
    - node_modules/
    - ~/.cache/ms-playwright/

playwright_tests:
  stage: test

  before_script:
    - yarn
    - npx playwright install --with-deps

  script:
    - yarn e2e

  artifacts:
    when: always
    paths:
      - playwright-report/
      - test-results/
      - allure-results/
      - allure-report/
      - results.xml
    expire_in: 1 week
```

---

## Explicação da pipeline

### image: node:24

Define a imagem Docker utilizada pelo runner.

Neste caso:

* Node.js versão 24

---

### stages

Define as etapas da pipeline.

```yml
stages:
  - test
```

A pipeline possui apenas a etapa de testes.

---

### cache

Utilizado para acelerar execuções futuras.

```yml
cache:
  paths:
    - node_modules/
    - ~/.cache/ms-playwright/
```

Itens armazenados:

* dependências Node
* navegadores instalados pelo Playwright

---

### playwright_tests

Nome do job executado.

---

### before_script

Executado antes dos testes.

```yml
before_script:
  - yarn
  - npx playwright install --with-deps
```

Comandos:

#### yarn

Instala dependências do projeto.

#### npx playwright install --with-deps

Instala:

* browsers
* dependências Linux necessárias para execução do Playwright

---

### script

Executa os testes automatizados.

```yml
script:
  - yarn e2e
```

O comando chama:

```json
"scripts": {
  "e2e": "npx playwright test"
}
```

---

### artifacts

Salva arquivos gerados após a execução.

```yml
artifacts:
  when: always
```

Os relatórios são preservados mesmo em caso de falha.

Arquivos salvos:

* playwright-report/
* test-results/
* allure-results/
* allure-report/
* results.xml

---

## Configuração do Playwright

Arquivo:

```bash
playwright.config.js
```

Configuração utilizada:

```javascript
export default defineConfig({
  testDir: './e2e',
  fullyParallel: true,
  forbidOnly: !!process.env.CI,
  retries: process.env.CI ? 2 : 0,
  workers: process.env.CI ? 1 : undefined,
  reporter: [
    ['html', { open: false }],
    ['junit', { outputFile: 'results.xml' }],
    ['allure-playwright']
  ],
  use: {
    baseURL: 'https://pgats-ci-example.netlify.app'
  }
})
```

---

## Resultado

A pipeline executa automaticamente:

1. Instala dependências
2. Instala browsers do Playwright
3. Executa testes E2E
4. Gera relatórios
5. Salva artifacts no GitLab

---

# Exercício 2 — Implementação de Plugin/Action do Marketplace

## Objetivo

Explorar plugins e ferramentas que agreguem valor ao fluxo da pipeline.

Ferramenta escolhida:

* entity["software","Allure Report","Allure Framework"]

---

## Motivo da escolha

O Allure foi escolhido por fornecer:

* relatórios visuais modernos
* histórico de execução
* detalhes completos de falhas
* rastreamento de steps
* screenshots e anexos
* melhor visualização dos testes

Além disso:

* é gratuito
* amplamente utilizado no mercado
* possui integração simples com Playwright

---

## Instalação

### Dependência do reporter

```bash
yarn add -D allure-playwright
```

---

### Instalação do Allure CLI

```bash
npm install -g allure-commandline --save-dev
```

---

### Necessidade do Java

O Allure depende do Java para geração do relatório.

Foi necessário instalar:

* Java JDK

Após instalação:

```bash
java -version
```

---

## Configuração no Playwright

Arquivo:

```bash
playwright.config.js
```

Reporter adicionado:

```javascript
reporter: [
  ['html', { open: false }],
  ['junit', { outputFile: 'results.xml' }],
  ['allure-playwright']
]
```

---

## Geração do relatório

### Executar testes

```bash
yarn e2e
```

---

### Gerar relatório Allure

```bash
npx allure generate allure-results --clean -o allure-report
```

---

### Abrir relatório

```bash
npx allure open allure-report
```

---

## Resultado obtido

O Allure gerou relatórios visuais contendo:

* status dos testes
* tempo de execução
* histórico
* retries
* falhas detalhadas
* traces
* organização mais profissional dos resultados

---

# Execução local

## Instalar dependências

```bash
yarn
```

---

## Instalar browsers do Playwright

```bash
npx playwright install --with-deps
```

---

## Executar testes

```bash
yarn e2e
```

---

## Abrir relatório HTML do Playwright

```bash
npx playwright show-report
```

---

## Gerar relatório Allure

```bash
npx allure generate allure-results --clean -o allure-report
```

---

## Abrir relatório Allure

```bash
npx allure open allure-report
```

---

# Versionamento

## Enviar alterações para GitLab

```bash
git add .
git commit -m "feat: adiciona pipeline CI e relatório Allure"
git push gitlab master
```

---

## Enviar alterações para GitHub

```bash
git push origin master
```

---

# Conceitos aprendidos

Durante os exercícios foram praticados:

* pipelines CI/CD
* GitLab CI
* runners
* artifacts
* cache
* Playwright
* testes E2E
* relatórios automatizados
* integração com Allure
* execução automatizada em ambiente Linux
* troubleshooting de dependências

---

# Autor

Projeto desenvolvido para fins acadêmicos e prática de Integração Contínua.
