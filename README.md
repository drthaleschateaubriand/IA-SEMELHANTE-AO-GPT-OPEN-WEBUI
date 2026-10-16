# Clara — assistente de textos local

Aplicação local, em português, para ajudar com textos curtos. Usa Ollama no próprio computador e SQLite para guardar conversas, memórias por conversa e instruções de agentes. Não há cadastro de usuários nem chamadas a serviços de IA em nuvem.

## O que já está incluído

- Acesso por uma única senha compartilhada, sem fluxo de cadastro ou recuperação de senha.
- Hash da senha com scrypt, salvo somente no arquivo local ignorado pelo Git (`.env`).
- Conversas salvas em `data/assistant.sqlite3`, com opção de excluir.
- Campo de memória editável por conversa, incluído como contexto quando a IA responde.
- Perfis de agentes com instruções reutilizáveis e seleção por conversa.
- Interface responsiva, sem dependências externas no navegador.
- Serviço escutando apenas em `127.0.0.1` por padrão.

## Preparação

1. Instale [Ollama](https://ollama.com/) no computador que executará o app e inicie o serviço.
2. Baixe o modelo padrão gratuito e local: `ollama pull qwen2.5:3b`. Ele ocupa alguns GB e a velocidade depende do computador.
3. No diretório do projeto, execute `./setup.sh` e informe a senha compartilhada escolhida.
4. Execute `./start.sh` e abra `http://127.0.0.1:8765`.

Para trocar o modelo, edite `OLLAMA_MODEL` em `.env` e baixe-o pelo Ollama. Para ajustar a porta, defina `APP_PORT` no `.env`.

## Dados e privacidade

O histórico e as memórias ficam no arquivo local `data/assistant.sqlite3`. As mensagens são enviadas apenas ao serviço Ollama local configurado em `OLLAMA_URL` (padrão `http://127.0.0.1:11434`). O app não criptografa o banco; proteja a conta do computador e faça cópias de segurança apenas em local aprovado. Não use dados identificáveis de pacientes sem validação e autorização da instituição. Não é um sistema de prontuário, não substitui protocolos clínicos e não valida decisões médicas.

O app está limitado ao computador onde é executado. Para acesso por outras pessoas/dispositivos, hospedagem pública ou uso institucional, é necessário configurar infraestrutura, proteção de transporte e controle de acesso apropriados; a senha compartilhada, sozinha, não fornece trilha de auditoria individual.

## Limites do custo

O software Ollama e os modelos abertos não cobram por requisição quando executados localmente. O custo recorrente de API é zero nesse modo, embora seja preciso ter um computador compatível, espaço em disco e energia. Não é possível garantir que hospedagem, serviços em nuvem ou os termos de modelos de terceiros continuem gratuitos para sempre; por isso este projeto não depende deles.
