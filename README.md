# reusable-workflows

:octocat: Coleção de **GitHub Actions Composite Actions** e **Reusable Workflows** para pipelines DevSecOps.

## Status dos Serviços

| Serviço | Status Page |
|---------|-------------|
| GitHub | https://www.githubstatus.com/ |
| Snyk | https://status.snyk.io/ |
| SonarCloud | https://sonarcloud.statuspage.io/ |
| Trivy (Aqua Security) | https://status.aquasec.com/ |
| Docker Hub | https://www.dockerstatus.com/ |
| GitHub Packages (GHCR) | https://www.githubstatus.com/ |

---

## Composite Actions

### DevSecOps / Security Tools

| Action | Descrição |
|--------|-----------|
| [`tools-trivy-scan`](.github/actions/tools-trivy-scan) | Scan de vulnerabilidades, licenças, secrets e misconfigurations com **Trivy** |
| [`tools-snyk-dotnet`](.github/actions/tools-snyk-dotnet) | Scan de segurança de container e dependências .NET com **Snyk** |
| [`tools-git-leaks`](.github/actions/tools-git-leaks) | Detecção de secrets no repositório com **GitLeaks** |
| [`tools-spectral`](.github/actions/tools-spectral) | Linting de OpenAPI specs com **Spectral CLI** (rulesets DevOps Linter + OWASP) |
| [`tools-sonar-cloud-dotnet`](.github/actions/tools-sonar-cloud-dotnet) | Análise de qualidade de código com **SonarCloud** |
| [`tools-safety`](.github/actions/tools-safety) | Verificação de vulnerabilidades em dependências Python com **Safety CLI** |
| [`tools-owasp-zap`](.github/actions/tools-owasp-zap) | Baseline scan com **OWASP ZAP** |

### Docker

| Action | Descrição |
|--------|-----------|
| [`tools-docker-setup`](.github/actions/tools-docker-setup) | Setup do ambiente Docker (QEMU + Buildx) |
| [`tools-docker-push`](.github/actions/tools-docker-push) | Build e push de imagens para qualquer container registry |
| [`tools-docker-check-image`](.github/actions/tools-docker-check-image) | Verificação se uma imagem já existe no registry |

### .NET

| Action | Descrição |
|--------|-----------|
| [`dotnet-get-version`](.github/actions/dotnet-get-version) | Extração de versão (Version, VersionPrefix, VersionSuffix) de um `.csproj` |
| [`dotnet-test`](.github/actions/dotnet-test) | Execução de testes com cobertura, geração de relatórios e upload de artefatos |

### Python

| Action | Descrição |
|--------|-----------|
| [`python-get-version`](.github/actions/python-get-version) | Extração de versão do projeto Python |
| [`python-code-quality`](.github/actions/python-code-quality) | Qualidade de código com flake8, black, isort, mypy |

### Node.js / React

| Action | Descrição |
|--------|-----------|
| [`node-get-package-data`](.github/actions/node-get-package-data) | Extração de versão do `package.json` |
| [`react-env-values`](.github/actions/react-env-values) | Criação de `.env` para aplicações React |

### Utilitários

| Action | Descrição |
|--------|-----------|
| [`github-tag`](.github/actions/github-tag) | Verificação e criação de tags Git |
| [`gist-badge`](.github/actions/gist-badge) | Atualização de badges via Gist (Shields.io) |

---

## Reusable Workflows

| Workflow | Descrição |
|----------|-----------|
| [`dotnet-sandbox-api-build.yml`](.github/workflows/dotnet-sandbox-api-build.yml) | Pipeline DevSecOps para APIs .NET — build, testes, scans de segurança, push de imagem |
| [`dotnet-sandbox-api-deploy-aca.yml`](.github/workflows/dotnet-sandbox-api-deploy-aca.yml) | Deploy de imagem para **Azure Container Apps** (.NET) |
| [`dotnet-pr-check.yml`](.github/workflows/dotnet-pr-check.yml) | Validação de PRs para projetos .NET |
| [`python-sandbox-api-build.yml`](.github/workflows/python-sandbox-api-build.yml) | Pipeline DevSecOps para APIs Python — build, testes, scans de segurança, push de imagem |
| [`python-sandbox-api-deploy-aca.yml`](.github/workflows/python-sandbox-api-deploy-aca.yml) | Deploy de imagem para **Azure Container Apps** (Python) |
| [`python-ci-cd-api.yml`](.github/workflows/python-ci-cd-api.yml) | CI/CD para APIs Python (legado — substituído pelos dois acima) |
| [`python-pr-check.yml`](.github/workflows/python-pr-check.yml) | Validação de PRs para projetos Python |
| [`react-sandbox-web-build.yml`](.github/workflows/react-sandbox-web-build.yml) | Pipeline DevSecOps para frontends React — build, scans de segurança, upload de artefato |
| [`react-sandbox-web-deploy-swa.yml`](.github/workflows/react-sandbox-web-deploy-swa.yml) | Deploy de artefato para **Azure Static Web Apps** + OWASP ZAP DAST |
| [`react-ci-cd-web.yml`](.github/workflows/react-ci-cd-web.yml) | CI/CD para aplicações React (legado — substituído pelos dois acima) |
| [`react-pr-check.yml`](.github/workflows/react-pr-check.yml) | Validação de PRs para projetos React |
| [`sandbox-console.yml`](.github/workflows/sandbox-console.yml) | Pipeline para aplicações console |

---

## Configuração do Repositório Caller

> **Pré-requisito:** Os **Environments** do GitHub (`DEV`, `HML`, `PRD` etc.) devem estar criados no repositório caller antes de executar qualquer pipeline de deploy. Acesse **Settings → Environments** e crie os ambientes correspondentes aos valores passados no input `environment`.

### `dotnet-sandbox-api-build.yml`

**Secrets** (Settings → Secrets and variables → Actions → Secrets):

| Nome | Obrigatório | Descrição |
|------|:-----------:|-----------|
| `GITLEAKS_LICENSE` | ✅ | Licença do GitLeaks |
| `SNYK_TOKEN` | ✅ | Token de autenticação do Snyk |
| `SONAR_TOKEN` | ✅ | Token de autenticação do SonarCloud |
| `SONAR_PROJECT_KEY` | ✅ | Chave do projeto no SonarCloud |
| `SAFETY_API_KEY` | ✅ | API Key do Safety CLI |
| `REGISTRY_PASSWORD` | ⬜ | Senha/token do registry. Omita para `ghcr.io` (usa `GITHUB_TOKEN` automaticamente) |

**Variables** (Settings → Secrets and variables → Actions → Variables):

| Nome | Obrigatório | Descrição |
|------|:-----------:|-----------|
| `SONAR_ORGANIZATION` | ✅ | Slug da organização no SonarCloud |

### `dotnet-sandbox-api-deploy-aca.yml`

**Secrets** (Settings → Secrets and variables → Actions → Secrets):

| Nome | Obrigatório | Descrição |
|------|:-----------:|-----------|
| `AZURE_CREDENTIALS` | ✅ | JSON com as credenciais do Service Principal Azure (saída de `az ad sp create-for-rbac`) |

**Variables** (Settings → Secrets and variables → Actions → Variables):

| Nome | Obrigatório | Descrição |
|------|:-----------:|-----------|
| `AZURE_RG` | ✅ | Base do nome do Resource Group (ex: `rg-myorg`) |
| `AZURE_ACAE_BASE` | ✅ | Base do nome do Container App Environment (ex: `cae-myorg`) |

### `python-sandbox-api-build.yml`

**Secrets** (Settings → Secrets and variables → Actions → Secrets):

| Nome | Obrigatório | Descrição |
|------|:-----------:|-----------|
| `GITLEAKS_LICENSE` | ✅ | Licença do GitLeaks |
| `GH_PACKAGES_TOKEN` | ✅ | Token do GitHub Packages para push de imagem |
| `CODECOV_TOKEN` | ⬜ | Token do Codecov para upload de cobertura |
| `BADGE_GIST_TOKEN` | ⬜ | Token do Gist para atualização do badge de CI/CD |
| `REGISTRY_PASSWORD` | ⬜ | Senha/token do registry. Omita para `ghcr.io` (usa `GH_PACKAGES_TOKEN` automaticamente) |

### `python-sandbox-api-deploy-aca.yml`

**Secrets** (Settings → Secrets and variables → Actions → Secrets):

| Nome | Obrigatório | Descrição |
|------|:-----------:|-----------|
| `AZURE_CREDENTIALS` | ✅ | JSON com as credenciais do Service Principal Azure (saída de `az ad sp create-for-rbac`) |

**Variables** (Settings → Secrets and variables → Actions → Variables):

| Nome | Obrigatório | Descrição |
|------|:-----------:|-----------|
| `AZURE_RG` | ✅ | Base do nome do Resource Group (ex: `rg-myorg`) |
| `AZURE_ACAE_BASE` | ✅ | Base do nome do Container App Environment (ex: `cae-myorg`) |

---

### `react-sandbox-web-build.yml`

**Secrets** (Settings → Secrets and variables → Actions → Secrets):

| Nome | Obrigatório | Descrição |
|------|:-----------:|-----------|
| `GITLEAKS_LICENSE` | ✅ | Licença do GitLeaks |
| `BADGE_GIST_TOKEN` | ⬜ | Token do Gist para atualização do badge CI/CD (somente em `main`) |
| `APPLICATIONINSIGHTS_CONNECTION_STRING` | ⬜ | Connection string do Application Insights (injetada no `.env`) |
| `VITE_AUTH_API_KEY` | ⬜ | Chave de API de autenticação (usada em repositórios específicos) |

**Variables** (Settings → Secrets and variables → Actions → Variables):

| Nome | Obrigatório | Descrição |
|------|:-----------:|-----------|
| `BADGE_GIST_ID` | ⬜ | ID do Gist para o badge CI/CD |
| `VITE_*` | ⬜ | Variáveis de ambiente do Vite (dependem do repositório e do environment) |

---

### `react-sandbox-web-deploy-swa.yml`

> **Pré-requisito:** O **Environment** GitHub (`DEV`, `HML`, `PRD` etc.) deve estar criado no repositório caller. As variáveis `AZURE_STATIC_WEBAPP_NAME` e `AZURE_RESOURCE_GROUP` devem ser definidas **dentro do Environment** correspondente.

**Secrets** (Settings → Secrets and variables → Actions → Secrets):

| Nome | Obrigatório | Descrição |
|------|:-----------:|-----------|
| `AZURE_CLIENT_ID` | ✅ | Client ID do Service Principal Azure para autenticação OIDC |
| `AZURE_TENANT_ID` | ✅ | Tenant ID do Azure AD para autenticação OIDC |
| `AZURE_SUBSCRIPTION_ID` | ✅ | Subscription ID do Azure para autenticação OIDC |
| `AZURE_STATIC_WEB_APPS_API_TOKEN` | ✅ | Token de deploy do Azure Static Web Apps |
| `BADGE_GIST_TOKEN` | ⬜ | Token do Gist para atualização do badge CI/CD |

**Variables** (Settings → Secrets and variables → Actions → Variables):

| Nome | Obrigatório | Descrição |
|------|:-----------:|-----------|
| `AZURE_STATIC_WEBAPP_NAME` | ✅* | Nome do recurso Azure Static Web App (necessário se `dist/config.json` tiver placeholders) |
| `AZURE_RESOURCE_GROUP` | ✅* | Nome do Resource Group do Azure Static Web App (necessário se `dist/config.json` tiver placeholders) |

> \* Obrigatório somente quando o arquivo `dist/config.json` do build contiver placeholders `{{ }}` que precisam ser preenchidos via app settings do Azure.

---

## Referências

- [Spectral CLI](https://meta.stoplight.io/docs/spectral/9ffa04e052cc1-spectral-cli)
- [dotnet test](https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-test?tabs=dotnet-test-with-vstest)
- [dotnet-coverage](https://learn.microsoft.com/en-us/dotnet/core/additional-tools/dotnet-coverage)
- [ReportGenerator](https://github.com/danielpalme/ReportGenerator) | [Usage](https://reportgenerator.io/usage)
- [Unit Testing Code Coverage](https://learn.microsoft.com/en-us/dotnet/core/testing/unit-testing-code-coverage?tabs=linux)
- [SonarCloud .NET Coverage Guide](https://community.sonarsource.com/t/coverage-troubleshooting-guide-for-net-code-coverage-import/37151)
- [SonarQube .NET Test Coverage](https://docs.sonarsource.com/sonarqube-server/latest/analyzing-source-code/test-coverage/dotnet-test-coverage/)
