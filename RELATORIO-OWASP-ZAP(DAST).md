Relatório de Varredura Dinâmica – OWASP ZAP (DAST)
📌 Objetivo

Executar testes dinâmicos de segurança no ambiente de staging utilizando o OWASP ZAP integrado ao pipeline de CD, com o intuito de identificar vulnerabilidades em tempo de execução, incluindo falhas de autenticação, exposição de dados e configurações inseguras.

🛠️ Ferramenta Utilizada

OWASP ZAP (Zed Attack Proxy) – Docker Stable

Executado de forma automatizada via GitHub Actions

📑 Sumário dos Resultados

Durante a varredura, foram identificados os seguintes achados de segurança:

Vulnerabilidade Detectada	Quantidade	Severidade (ZAP)
Cross-Domain JavaScript Source File Inclusion (10017)	10	Medium
Information Disclosure - Suspicious Comments (10027)	2	Medium
Content Security Policy (CSP) Header Not Set (10038)	11	High
Non-Storable Content (10049)	11	Low
Deprecated Feature Policy Header Set (10063)	11	Low
Timestamp Disclosure - Unix (10096)	8	Low
Cross-Domain Misconfiguration (10098)	11	Medium
Modern Web Application (10109)	11	Info
Dangerous JS Functions (10110)	2	Medium
Insufficient Site Isolation Against Spectre (90004)	10	Medium

✅ Total de Achados: 87
⚠️ Falhas Críticas: Não foram encontradas falhas classificadas como Critical.
⚠️ Falhas Altas (High): 1 vulnerabilidade principal (CSP Header Not Set).

🔍 Evidências e Exemplos

Content Security Policy (CSP) Header Not Set

Evidência: Aplicação não retornou o cabeçalho Content-Security-Policy.

Risco: Aumenta a superfície para ataques de XSS e injeção de conteúdo.

Mitigação: Configurar o servidor web para incluir o cabeçalho, por exemplo:

Content-Security-Policy: default-src 'self'; script-src 'self'


Cross-Domain JavaScript Source File Inclusion

Evidência: Inclusão de scripts externos de domínios não confiáveis.

Risco: Possibilidade de execução de código malicioso injetado por terceiros.

Mitigação: Restringir fontes de scripts confiáveis usando CSP e revisar dependências externas.

Information Disclosure - Suspicious Comments

Evidência: Comentários no código HTML/JS expuseram informações possivelmente sensíveis.

Mitigação: Remover comentários de produção que contenham caminhos, credenciais ou lógica de autenticação.

Dangerous JS Functions

Evidência: Funções como eval() e document.write() foram detectadas.

Mitigação: Evitar uso de funções perigosas, substituir por alternativas seguras.

Insufficient Site Isolation Against Spectre

Evidência: Cabeçalhos de isolamento de site não configurados.

Mitigação: Configurar cabeçalhos como Cross-Origin-Opener-Policy e Cross-Origin-Embedder-Policy.

📌 Conclusão

A análise dinâmica detectou 87 achados, em sua maioria médios e baixos, sendo o mais relevante a ausência do cabeçalho CSP.
Embora nenhuma falha crítica tenha sido identificada, recomenda-se priorizar:

Configuração de Content Security Policy (CSP).

Revisão de scripts externos e remoção de funções JS inseguras.

Ajuste de cabeçalhos de segurança (CSP, COOP, COEP).

Remoção de comentários de código expostos em produção.

📤 Esse relatório deve ser anexado como parte da entrega da Tarefa 2.
