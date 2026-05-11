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
| [`dotnet-sandbox-api.yml`](.github/workflows/dotnet-sandbox-api.yml) | Pipeline DevSecOps completa para APIs .NET (build, test, scan, push) |
| [`dotnet-pr-check.yml`](.github/workflows/dotnet-pr-check.yml) | Validação de PRs para projetos .NET |
| [`python-ci-cd-api.yml`](.github/workflows/python-ci-cd-api.yml) | CI/CD para APIs Python |
| [`python-pr-check.yml`](.github/workflows/python-pr-check.yml) | Validação de PRs para projetos Python |
| [`react-ci-cd-web.yml`](.github/workflows/react-ci-cd-web.yml) | CI/CD para aplicações React |
| [`react-pr-check.yml`](.github/workflows/react-pr-check.yml) | Validação de PRs para projetos React |
| [`sandbox-console.yml`](.github/workflows/sandbox-console.yml) | Pipeline para aplicações console |

---

## Referências

- [Spectral CLI](https://meta.stoplight.io/docs/spectral/9ffa04e052cc1-spectral-cli)
- [dotnet test](https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-test?tabs=dotnet-test-with-vstest)
- [dotnet-coverage](https://learn.microsoft.com/en-us/dotnet/core/additional-tools/dotnet-coverage)
- [ReportGenerator](https://github.com/danielpalme/ReportGenerator) | [Usage](https://reportgenerator.io/usage)
- [Unit Testing Code Coverage](https://learn.microsoft.com/en-us/dotnet/core/testing/unit-testing-code-coverage?tabs=linux)
- [SonarCloud .NET Coverage Guide](https://community.sonarsource.com/t/coverage-troubleshooting-guide-for-net-code-coverage-import/37151)
- [SonarQube .NET Test Coverage](https://docs.sonarsource.com/sonarqube-server/latest/analyzing-source-code/test-coverage/dotnet-test-coverage/)
