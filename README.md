# Relatorio_bancocn

Sobre o projeto

Este repositório documenta um estudo prático de segurança em aplicações web realizado no laboratório BancoCN. O objetivo foi exercitar reconhecimento, identificação e validação de vulnerabilidades, análise de impacto e elaboração de recomendações técnicas.

Escopo: atividade apresentada como educacional, em ambiente de laboratório. Este trabalho não representa um pentest contratado nem uma auditoria completa.

Metodologia e atividades realizadas

Reconhecimento passivo: consultas WHOIS e buscas indexadas com Google Dorking.

Mapeamento inicial: consulta ao robots.txt e observação de rotas e recursos da aplicação.

Identificação de tecnologias: análise de respostas e uso do Wappalyzer; foram observados indícios relacionados a MySQL/MariaDB, sem confirmação da configuração do servidor.

Validação de SQL Injection: análise de erro de sintaxe SQL e resposta compatível com a técnica UNION-based.

Análise do upload: avaliação da aceitação de extensões, incluindo arquivo .php5.

Comprovação de execução: retorno de www-data ao comando de verificação whoami, indicando execução com os privilégios da conta do servidor web.

Principais achados

BCN-01 — SQL Injection (UNION-based)

Evidência: mensagem de erro SQL e resposta contendo informações associadas a uma conta administrativa, incluindo um hash de senha (omitido da versão pública).

Impacto observado: exposição de informações na resposta da aplicação.

Mitigações recomendadas: consultas parametrizadas, validação de entradas, mensagens de erro genéricas e menor privilégio no acesso ao banco de dados.

BCN-02 — Upload inseguro com execução remota de comandos (RCE)

Evidência: aceitação e execução de arquivo com extensão .php5; resposta www-data à verificação com whoami.

Impacto observado: execução de comandos no contexto da conta do serviço web.

Mitigações recomendadas: lista restrita de tipos permitidos, validação de conteúdo, armazenamento de uploads fora do diretório público, bloqueio de execução de scripts na pasta de uploads e permissões mínimas.

Limite das evidências: os registros não demonstram acesso root, elevação de privilégios ou que a SQL Injection tenha sido necessariamente usada para alcançar o recurso de upload. As avaliações de severidade do relatório são qualitativas, sem pontuação CVSS formal.

Relatório completo e evidências

Abrir o relatório técnico em PDF

O documento apresenta as capturas de tela, a descrição dos achados, os impactos observados e as recomendações de mitigação. Dados de credenciais, domínio e parâmetros sensíveis foram omitidos da versão pública.

Conhecimentos demonstrados

Reconhecimento passivo e enumeração de recursos web.

Análise e validação de vulnerabilidades em aplicações web.

Interpretação de evidências de SQL Injection e upload inseguro.

Documentação técnica e recomendações de mitigação.

Comunicação de limitações e do impacto efetivamente observado.

Uso responsável

Este material destina-se exclusivamente a estudo e portfólio profissional. Não realize testes em sistemas sem autorização. Nenhuma credencial, hash de senha ou caminho funcional de web shell é fornecido neste repositório.
