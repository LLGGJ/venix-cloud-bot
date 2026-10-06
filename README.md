# filepath: README.md
# VenixCloud Discord Bot

Bot oficial de gerenciamento para hospedagens **VenixCloud**, construído com **Discord.js v14+** e **Components V2**. Permite criar, gerenciar, monitorar e fazer deploy de aplicações diretamente pelo Discord.

> ⚠️ **Nota:** Este bot depende de uma API externa (VenixCloud) e de um site de autenticação OAuth2 separado. Certifique-se de ter acesso às credenciais da API antes de iniciar.

## 🚀 Funcionalidades

- **Interface Moderna:** 100% baseado em Discord Components V2 (Sem Embeds tradicionais).
- **Slash Commands:** Todos os comandos registrados via Slash (`/`).
- **Gerenciamento de Apps:** Criar, iniciar, parar, reiniciar, deletar e alterar recursos (RAM).
- **Deploy Automático:** Suporte a upload de `.zip` e integração com GitHub.
- **Logs em Tempo Real:** Visualização de logs via Stream (SSE).
- **Segurança:** Tokens criptografados (AES-256-GCM) e sessão persistente via MongoDB.
- **Auto-Renovação:** Sistema robusto de refresh token para evitar desconexões.

## 🛠️ Pré-requisitos

- [Node.js](https://nodejs.org/) v18 ou superior.
- [MongoDB](https://www.mongodb.com/) (Atlas recomendado para produção).
- Uma conta na **VenixCloud** com acesso à API.
- Um site hospedado (ex: Vercel) para o fluxo de OAuth2 (repositório irmão `website`).

## 📦 Instalação e Configuração

Siga estes passos para rodar o bot localmente ou em um servidor.

### 1. Clonar o Repositório

