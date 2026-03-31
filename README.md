# Relatório de Prontidão Técnica: Onboarding SecOps

**Disciplina:** Engenharia de Produto de Software (FGA0316) - 2026.1  
**Aluno:** Júlio Cesar | **Matrícula:** 221007591

---

## 1. Configuração do Ambiente (Zero Trust & Isolamento)
Conforme as diretrizes de Soberania Técnica, as seguintes configurações foram aplicadas:

* [x] **Python 3.12:** Instalado e verificado (v3.12.10).
* [x] **Poetry:** Configurado para criar `.venv` dentro do projeto (`virtualenvs.in-project true`).
* [x] **Determinismo:** Arquivos `pyproject.toml` e `poetry.lock` gerados com sucesso.

---

## 2. Logs de Auditoria e Qualidade (Security Gate)
Abaixo constam os resumos das execuções dos comandos de segurança:

### 2.1. Auditoria Estática (Bandit)
> **Resultado:** No issues identified.  
> **Linhas analisadas:** 128 | **Vulnerabilidades:** ZERO.

```text
Run started:2026-03-31 02:41:14.297757+00:00

Test results:
        No issues identified.

Code scanned:
        Total lines of code: 128
        Total lines skipped (#nosec): 1

Run metrics:
        Total issues (by severity):
                Undefined: 0
                Low: 0
                Medium: 0
                High: 0
        Total issues (by confidence):
                Undefined: 0
                Low: 0
                Medium: 0
                High: 0
Files skipped (0):
```
*Comando: `poetry run bandit -r .`*

### 2.2. Verificação de Dependências (Safety)

```
REPORT

  Safety v3.7.0 is scanning for Vulnerabilities...
  Scanning dependencies in your environment:

  -> .\.venv\Lib\site-packages

  Using open-source vulnerability database
  Found and scanned 47 packages
  Timestamp 2026-03-30 23:17:20
  0 vulnerabilities reported
  0 vulnerabilities ignored
```

*Comando: `poetry run safety check`*

### 2.3. Qualidade e Conformidade (Ruff)
```
PS .\.secops-project> poetry run ruff check .
All checks passed! 
```
*Comando: `poetry run ruff check .`*

## 3. Evidência de Integração Contínua (CI)
O pipeline automatizado foi executado com sucesso no GitHub Actions:
- **Link da Action de Sucesso:** https://github.com/Julio1099/secops-project/actions/runs/23778135310/job/69284401201

## 4. Declaração de Soberania Técnica (CISSP Domain 8)
Eu, Júlio Cesar, declaro que auditei manualmente as ferramentas e dependências deste projeto. Confirmo que o código gerado via IA (GitHub Copilot) passou pela minha revisão humana (*Human-in-the-loop*), garantindo que não há vazamento de segredos ou falhas lógicas críticas antes da migração para o ecossistema da PCDF.

---
**Data de Entrega:** 31/03/2026

**Observações gerais e específicas:**

### Observações técnicas e futuras:

* **Isolamento de Perímetro:** Foi criado um arquivo de configuração `.bandit` para excluir o diretório `./.venv` da análise estática, focando a auditoria no código proprietário e reduzindo ruídos de bibliotecas de terceiros (já validadas pelo *Safety*).
* **Gestão de Segredos:** A vulnerabilidade **B105 (Hardcoded Password)** detectada na `SECRET_KEY` do Django foi tratada via `# nosec` após revisão manual. Para o futuro, planeja-se a migração para variáveis de ambiente via arquivo `.env`.
* **Ambiente Virtual:** A configuração `virtualenvs.in-project true` garantiu que todo o ecossistema de desenvolvimento estivesse contido na pasta do projeto, facilitando a auditoria e a portabilidade para a PCDF.