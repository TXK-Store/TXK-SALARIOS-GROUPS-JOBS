Aqui está um exemplo de um README para o seu script de pagamento automático para trabalhos e grupos VIP em RedM. Esse README inclui detalhes essenciais para que desenvolvedores entendam como configurar e usar o script no futuro.

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

---

## Observações

- **Integração com VORP**: Certifique-se de que o framework VORP está instalado corretamente.
- **Pagamento em Intervalos Fixos**: O intervalo de pagamento é global. Todos os jogadores receberão o pagamento ao mesmo tempo, independentemente do momento de login.

---

## Contribuição

Desenvolvedores futuros podem personalizar e expandir este script conforme necessário. Sugestões para melhorias e correções são sempre bem-vindas.
