# TODO / Ideias anotadas

## ✅ Já implementado
- Todos os comandos migrados para Slash Commands (prefixo `.` removido).
- `/login` migrado para o site: OAuth2 + PKCE direto com a VenixCloud
  (não com o Discord — o Discord só é usado para identificar quem pediu,
  via um token assinado embutido no link). Sem mais tópicos de login.
- Renovação automática de token (`access_token` via `refresh_token`) em
  `services/api.js -> getValidAccessToken()`, usada por todos os comandos
  que chamam a API da VenixCloud.
- Banco de dados migrado para MongoDB Atlas (compartilhado entre bot e site).
- Criptografia AES-256-GCM dos tokens salvos (`services/crypto.js`).
- `/apps`: listagem + gerenciamento (reiniciar, iniciar, renomear, alterar memória, ver logs).
- Timeout automático de tópico do `/up` (10 min) + trava de "1 tópico por vez".
- Emojis customizados automáticos (`services/emojiSync.js`) — gerados de ícones Lucide.
- /up agora checa login ANTES de mostrar qualquer painel público (antes mostrava
  "Carregando..." publicamente até descobrir que o usuário não estava conectado).
- /apps: opções de excluir aplicação (com confirmação) e "Novo commit" (tópico + upload
  de .zip -> POST /files/upload + POST /files/extract, confirmados na doc, + restart automático).
- Sistema de recuperação de sessão em 3 camadas (renovação sob demanda com trava/retentativas,
  retry em erro de autenticação, renovação em segundo plano) + DM avisando quando expira de vez.
- Botão "Conectar" fora do container em todo aviso de sessão expirada/não conectado.
- `/apps`: opções de criar backup (`POST /snapshots`) e deploy via GitHub (`POST /apps/:id/deploy/trigger`).
- Paginação do `/ajuda` corrigida (página de destino codificada no customId do botão, não "lida de volta").
- Confirmação antes de ações destrutivas no `/apps` (reiniciar, renomear, alterar memória).
- DM automática após login concluído (`services/dmNotifier.js`, por polling, opcional).
- API atualizada contra a documentação oficial da VenixCloud: `runtime`/`isWeb`/`subdomain`
  agora são enviados no `/up` (eram obrigatórios e faltavam); `start`/`stop`/`restart` unificados
  no endpoint real `POST /apps/:id/action`; `updateAppRam()` corrigido pra `max_ram`;
  `deleteApp()` confirmado; `getAppLogs()` migrado pra ler o SSE stream real (`/instances/stream/:id`).

## 🔴 Pendente de decisão (depende do dono da API / documentação)
- `renameApp()` provavelmente **não é suportado** — a doc do `PATCH /apps/:id` só lista
  `max_ram`, `startCommand`, `runtime`, sem campo pra nome. Perguntar se existe outra forma.
- `getAppLogs()` lê o SSE stream (`/instances/stream/:id`) só extraindo linhas `data:` —
  o formato exato de cada evento (nomes de `event:`, se logs vêm só em `data:`) não foi
  detalhado na doc. Testar contra o stream real e ajustar o parser se necessário.
- O formato de renovação de token (`grant_type=refresh_token` em
  `POST /oauth2/token`) foi assumido igual ao exchange original — não foi
  mostrado explicitamente no exemplo de integração fornecido. Confirmar.
- Onde exatamente cadastrar o "app OAuth2" na VenixCloud para conseguir o
  `VENIX_OAUTH_CLIENT_ID`/`VENIX_OAUTH_CLIENT_SECRET`? (provavelmente um
  painel de desenvolvedor em venixcloud.com, mas não confirmado).

## 💡 Ideias para adicionar depois
- Comando `/logout` — desconectar a conta VenixCloud (apagar sessão do Mongo).
- Comando admin (`/stats`) — quantos usuários conectados, deploys recentes, etc.
- Log de auditoria (canal privado) para ações de `/up` e ações destrutivas do `/apps`.
- Botão "🔄 Atualizar" no `/apps` para reconsultar status sem rodar o comando de novo.
