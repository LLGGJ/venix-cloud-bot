# filepath: SECURITY.md
# Política de Segurança

## Relatando Vulnerabilidades

Se você descobrir uma vulnerabilidade de segurança neste projeto, por favor, envie um e-mail para **[SEU_EMAIL_AQUI]**. Não abra uma Issue pública no GitHub para problemas de segurança críticos.

## Melhores Práticas para Contribuidores

1. **Nunca commite credenciais:** Verifique sempre que não há tokens, chaves de API ou senhas no seu código antes de enviar um Pull Request.
2. **Use Variáveis de Ambiente:** Todas as configurações sensíveis devem ser lidas via `process.env`.
3. **Validação de Entrada:** Sempre valide inputs de usuários, especialmente em comandos que interagem com a API externa.

## Configuração Segura

Ao rodar sua própria instância:
- Gere uma `ENCRYPTION_KEY` única.
- Restrinja o acesso ao banco de dados MongoDB por IP.
- Mantenha as dependências atualizadas (`npm audit fix`).
