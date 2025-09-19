# Documentação do Pipeline CI/CD com Integração de Segurança

## 📌 Objetivo
Consolidar as práticas de **SAST**, **DAST** e **SCA** em um pipeline de CI/CD unificado, garantindo que a aplicação seja validada automaticamente contra falhas de segurança a cada alteração de código.

---

## 🔄 Fluxo do Pipeline

1. **Trigger Automático**  
   - O pipeline é disparado em cada `commit` ou `pull request`.

2. **Estágio 1 – SAST (Static Application Security Testing)**  
   - Ferramenta: **Semgrep**  
   - Finalidade: análise estática do código-fonte para identificar más práticas, vulnerabilidades de lógica e uso inseguro de funções.  
   - Saída: `relatorio_sast.md`  

3. **Estágio 2 – DAST (Dynamic Application Security Testing)**  
   - Ferramenta: **OWASP ZAP**  
   - Finalidade: varredura da aplicação em execução em ambiente de staging.  
   - Verifica: autenticação, endpoints expostos, configurações inseguras.  
   - Saída: `relatorio_dast.md`  

4. **Estágio 3 – SCA (Software Composition Analysis)**  
   - Ferramenta: **OWASP Dependency-Check**  
   - Finalidade: análise de bibliotecas externas utilizadas no projeto.  
   - Verifica: CVEs conhecidos, versões desatualizadas, problemas de licenciamento.  
   - Saída: `RELATORIO_SCA.md`  

5. **Estágio 4 – Políticas de Segurança**  
   - Deploy é **bloqueado automaticamente** caso:  
     - Vulnerabilidades **críticas** sejam encontradas no SAST.  
     - Vulnerabilidades **altas** sejam encontradas no DAST ou SCA.  

6. **Estágio 5 – Notificações e Monitoramento**  
   - Alertas enviados via **GitHub Actions Summary** e/ou integração com **Slack/Teams**.  
   - Relatórios armazenados em pasta `reports/` no repositório.  
   - Logs disponíveis no histórico do pipeline.  

---

## ⚙️ Exemplo de Arquitetura do Workflow

```yaml
name: Security CI/CD

on:
  push:
    branches: [ "main" ]
  pull_request:

jobs:
  sast:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run Semgrep SAST
        run: semgrep --config=auto --json > reports/sast.json

  dast:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run OWASP ZAP DAST
        uses: zaproxy/action-full-scan@v0.8.0
        with:
          target: "http://localhost:3000"
          allow_issue_writing: false
          cmd_options: "-a -j -m 3"

  sca:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run Dependency-Check SCA
        uses: dependency-check/Dependency-Check_Action@main
        with:
          project: "MeuProjeto"
          path: "."
          format: "ALL"
          out: "reports"

  security-policy:
    runs-on: ubuntu-latest
    needs: [sast, dast, sca]
    steps:
      - name: Block Deploy if Critical Issues Found
        run: |
          echo "Implementar lógica de bloqueio com base nos relatórios"


📊 Dashboards e Monitoramento Contínuo

Integração com ferramentas de monitoramento (SonarQube, DefectDojo, ou GitHub Security Dashboard).

Relatórios versionados no repositório em reports/.

Histórico disponível para auditoria e conformidade.

✅ Conclusão

Este pipeline garante que cada entrega de software passe obrigatoriamente por validações de segurança em três camadas: código-fonte (SAST), execução (DAST) e dependências (SCA).
Dessa forma, a equipe reduz riscos, aumenta a confiabilidade da aplicação e promove a segurança contínua no ciclo de vida do desenvolvimento.
