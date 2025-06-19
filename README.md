
---

# RedM Job & Group Payment Script

Este script foi desenvolvido para o framework VORP no RedM e permite configurar salários automáticos para trabalhos e grupos, com intervalos definidos. Ele foi criado para oferecer suporte a grupos VIP e garantir que os pagamentos sejam distribuídos apenas a trabalhos e grupos especificados no arquivo de configuração.

## Funcionalidades

- **Pagamento Automático**: Distribui salários automaticamente para jogadores com base no trabalho e/ou grupo a que pertencem.
- **Configuração de Intervalo Global**: Define um intervalo fixo de tempo entre pagamentos.
- **Suporte a VIP**: Configura grupos VIP com salários personalizados.
- **Personalizável**: Facilita a configuração de salários e permissões através do arquivo `Config.lua`.

---

## Instalação

1. **Baixe e Extraia**: Baixe o arquivo do script e extraia-o na pasta `resources` do seu servidor.
2. **Renomeie a Pasta** (opcional): Renomeie a pasta extraída para um nome de sua escolha (por exemplo, `TXK_salario_jobs_group`).
3. **Adicione no `server.cfg`**: Adicione o recurso ao seu arquivo `server.cfg` para garantir que o script seja iniciado com o servidor:

   ```plaintext
   ensure TXK_salario_jobs_group
   ```

---

## Configuração

### Arquivo `Config.lua`

Edite o arquivo `Config.lua` para definir salários para cada trabalho e grupo. Abaixo está um exemplo de configuração:

```lua
Config = {}

-- Configuração de salários para cada trabalho
Config.Jobs = {
    ["police"] = 2,          -- Trabalho de policial recebe $2
    ["doctor"] = 2,          -- Trabalho de médico recebe $2
    ["farmer"] = 2,          -- Trabalho de fazendeiro recebe $2
}

-- Configuração de salários para cada grupo
Config.Groups = {
    ["admin"] = 1,           -- Grupo de administração recebe $1
    ["moderator"] = 1,       -- Grupo de moderadores recebe $1

    -- Grupos VIP com salários personalizados
    ["vip_bronze"] = 5,
    ["vip_prata"] = 10,
    ["vip_ouro"] = 15,
    ["vip_diamante"] = 20,
}

-- Intervalo global de pagamento em segundos
Config.PaymentInterval = 3600  -- Intervalo de 1 hora
```

---

## Como Funciona

1. **Verificação de Permissão**: O script verifica se o trabalho ou grupo do jogador está listado em `Config.Jobs` ou `Config.Groups`.
2. **Distribuição de Pagamento**: Jogadores permitidos recebem o valor configurado em seu trabalho ou grupo, em intervalos definidos por `Config.PaymentInterval`.
3. **Notificação**: Uma mensagem é exibida no jogo informando o jogador sobre o pagamento recebido.

### Arquivo `server.lua`

O `server.lua` controla a lógica de distribuição de salários e verifica permissões. Ele utiliza o evento `VorpCore.getUser` para obter os dados do jogador e verifica se ele é elegível para o pagamento.

---

## Exemplo de Expansão

Para adicionar mais trabalhos ou grupos, basta editar o `Config.lua`:

```lua
Config.Jobs["miner"] = 3        -- Novo trabalho de minerador com salário de $3
Config.Groups["vip_esmeralda"] = 25 -- Novo grupo VIP "Esmeralda" com salário de $25
```

## Como configurar o webhook do Discord

### 1. Criar o Webhook no Discord

1. Vá para o canal do Discord onde você quer receber as notificações
2. Clique com o botão direito no canal
3. Selecione "Editar Canal"
4. Vá para a aba "Integrações"
5. Clique em "Webhooks"
6. Clique em "Novo Webhook"
7. Dê um nome ao webhook (ex: "Sistema de Salários")
8. Copie a URL do webhook

### 2. Configurar no arquivo config.lua

Abra o arquivo `config.lua` e localize a seção `Config.Discord`:

```lua
Config.Discord = {
    WebhookURL = "SUA_URL_DO_WEBHOOK_AQUI", -- Cole a URL do webhook aqui
    BotName = "Sistema de Salários", -- Nome do bot que enviará as mensagens
    BotAvatar = "", -- URL do avatar do bot (opcional)
    Enabled = true, -- Habilita/desabilita o webhook
    Color = 0x00ff00, -- Cor da embed (verde)
    FooterText = "Sistema de Salários TXK", -- Texto do rodapé da embed
    FooterIcon = "", -- Ícone do rodapé (opcional)
    
    -- Mensagens personalizáveis
    Messages = {
        SalaryPaid = "💰 Salário pago com sucesso!",
        JobSalary = "💼 Salário de trabalho recebido",
        GroupSalary = "👑 Salário VIP recebido",
        SteamSalary = "🎮 Salário especial recebido"
    }
}
```

### 3. Personalização

#### Cores disponíveis:
- `0x00ff00` - Verde
- `0xff0000` - Vermelho
- `0x0000ff` - Azul
- `0xffff00` - Amarelo
- `0xff00ff` - Magenta
- `0x00ffff` - Ciano
- `0xffffff` - Branco
- `0x000000` - Preto

#### Exemplo de configuração personalizada:

```lua
Config.Discord = {
    WebhookURL = "https://discord.com/api/webhooks/123456789/abcdef...",
    BotName = "🏦 Banco Central",
    BotAvatar = "https://exemplo.com/avatar.png",
    Enabled = true,
    Color = 0x00ff00,
    FooterText = "🏆 Servidor TXK - Sistema de Salários",
    FooterIcon = "https://exemplo.com/icon.png",
    
    Messages = {
        SalaryPaid = "🎉 Salário depositado na conta!",
        JobSalary = "💼 Pagamento de trabalho realizado",
        GroupSalary = "👑 Benefício VIP creditado",
        SteamSalary = "🎮 Bônus especial depositado"
    }
}
```

### 4. Desabilitar o webhook

Para desabilitar o webhook, você pode:

1. Deixar o `WebhookURL` vazio: `WebhookURL = ""`
2. Ou definir `Enabled = false`

### 5. Informações enviadas no webhook

O webhook enviará as seguintes informações:
- **Nome do jogador**
- **Valor do salário**
- **Tipo de salário** (trabalho, grupo VIP, ou Steam ID especial)
- **Trabalho** (se aplicável)
- **Grupo** (se aplicável)
- **📋 Identificação:**
  - **Discord:** @ do jogador (menciona o usuário)
  - **Steam:** Steam ID do jogador
  - **Character ID:** ID do personagem no banco de dados
- **Data e hora** do pagamento

### 6. Exemplo de mensagem no Discord

```
💰 Salário pago com sucesso!

Jogador: John Doe
Valor: $50
Tipo: 👑 Salário VIP recebido
Grupo: Ouro

📋 Identificação:
Discord: @JohnDoe#1234
Steam: steam:110000108695de4
Character ID: 12345
```

### 7. Funcionalidades de Identificação

#### Discord ID (@ do jogador)
- O sistema automaticamente detecta o Discord ID do jogador
- Usa a formatação `<@ID>` para mencionar o jogador no Discord
- Se o jogador não tiver Discord conectado, não será exibido

#### Steam ID
- Mostra o Steam ID completo do jogador
- Útil para identificação e logs administrativos
- Formato: `steam:110000108695de4`

#### Character ID
- ID único do personagem no banco de dados VORP
- Útil para consultas administrativas e logs
- Formato: `12345`

### 8. Troubleshooting

Se o webhook não estiver funcionando:

1. Verifique se a URL do webhook está correta
2. Certifique-se de que `Enabled = true`
3. Verifique se o webhook ainda existe no Discord
4. Teste a URL do webhook em um serviço como webhook.site
5. Verifique se o jogador tem Discord conectado para receber menções

### 9. Segurança

⚠️ **Importante**: 
- Nunca compartilhe a URL do webhook publicamente, pois ela pode ser usada para enviar mensagens no seu canal do Discord
- As informações de identificação são úteis para administradores, mas devem ser tratadas com confidencialidade
- O Discord ID permite mencionar jogadores diretamente no canal 
---

## Observações

- **Integração com VORP**: Certifique-se de que o framework VORP está instalado corretamente.
- **Pagamento em Intervalos Fixos**: O intervalo de pagamento é global. Todos os jogadores receberão o pagamento ao mesmo tempo, independentemente do momento de login.

---

## Contribuição

Desenvolvedores futuros podem personalizar e expandir este script conforme necessário. Sugestões para melhorias e correções são sempre bem-vindas.
