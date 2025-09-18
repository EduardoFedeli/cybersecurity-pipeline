# cybersecurity-pipeline

📄 Relatório de SAST – Análise Estática de Código
📌 Informações Gerais

Projeto: Cybersecurity Pipeline

Data da Análise: 17/09/2025

Ferramenta Utilizada: Semgrep (GitHub Actions CI)

Pipeline: Execução automática em push e pull_request

Link do github: https://github.com/EduardoFedeli/cybersecurity-pipeline

🔎 Resumo da Análise

Total de arquivos analisados: 45

Total de vulnerabilidades encontradas: 0

Classificação por severidade:

🔴 Críticas: 0

🟠 Altas: 0

🟡 Médias: 0

🟢 Baixas: 0

📊 Detalhamento das Vulnerabilidades

Não foram encontradas vulnerabilidades pelo Semgrep nesta execução do pipeline.

✅ Conclusão

A análise estática com Semgrep não detectou nenhuma vulnerabilidade no código nesta execução.
Isso indica que, até o momento, o código está seguindo boas práticas básicas de segurança.

Recomendações:

Continuar executando o pipeline de SAST a cada commit/pull request.

Revisar manualmente mudanças críticas de segurança no código.

Manter dependências e bibliotecas atualizadas.

Incluir outros testes de segurança (DAST e SCA) nas próximas sprints, conforme planejado.

📂 Evidências

O workflow de SAST foi executado com sucesso no GitHub Actions.

Artefato semgrep-findings foi gerado, confirmando que o pipeline rodou, mesmo sem vulnerabilidades detectadas.

O arquivo SARIF (semgrep.sarif) também foi criado e enviado para GitHub Code Scanning.