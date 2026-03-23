# 📋 Plano de Reestruturação de Leads — Padrão ISO e Inferência

Este documento propõe as ações finais para elevar a qualidade do ficheiro `Leads_Limpos_Zoho_2026_03_23.xlsx` a **Padrão ISO** de qualidade de dados, aplicando técnicas avançadas de inferência de dados cruzados.

## 🛠 Ações Propostas

### 1. Nomes em Formato Padrão (Inferência de "Lead Name")
A maioria das ferramentas de e-mail marketing (como o Zoho Campaigns ou ActiveCampaign) exige o **Nome (First Name)** para personalização ("Olá [Nome]").
- **O Problema:** Identifiquei 31.444 leads sem `Nome` e `Sobrenome` separados, mas que têm o campo `Lead Name` preenchido (ex: "Maria Silva Santos").
- **A Solução:** Separar a primeira palavra para o campo `Nome` e o restante para `Sobrenome`.
- **Extra:** Aplicar "Title Case" para garantir que fica `Maria` e não `MARIA` ou `maria`.

### 2. Datas em Padrão ISO 8601 ⏱️
O Zoho e a maioria dos CRMs utilizam o padrão internacional ISO 8601 para evitar confusões entre dias e meses (típico entre o formato americano e europeu).
- **O Problema:** Existem 13 colunas de data/hora (ex: `Hora de Criação`, `Data da última movimentação`) com formatos de texto variados.
- **A Solução:** Converter absoluta e rigorosamente todos os campos de data para o padrão `YYYY-MM-DD HH:MM:SS`.

### 3. Fontes de Leads (Inferência RD Station ➔ Zoho) 🚀
Muitos leads entram por integrações externas (RD Station, Meta Ads) e não mapeiam a fonte correta no Zoho.
- **O Problema:** O campo `Fonte de Lead` está vazio para muitos leads, mas o campo `Origem da primeira conversão` tem dados ricos (ex: `Busca Paga | Facebook Ads`). Há mais de **20.448 leads** nesta situação.
- **A Solução:** Se a `Fonte de Lead` estiver vazia, preencher através de um mapeamento Inteligente:
  - `Busca Paga | Facebook Ads` ➔ `Meta ADS`
  - `Busca Paga | google` ➔ `Google ADS`
  - `Busca Orgânica | Google` ➔ `SEO Orgânico`
  - `Outros | paid` ➔ `Tráfego Pago`

### 4. Telefones em Norma Internacional E.164 📞
Embora já se tenha colocado o `+` e o indicativo na fase anterior, vamos finalizar a norma E.164 absoluta.
- **A Solução:** Garantir que todos os valores das colunas `Celular` e `Telefone` começam com `+` e contêm apenas dígitos a seguir (sem espaços ocultos que quebrem os SMS automáticos e o WhatsApp). O E-mail será todo transformado em *lowercase* e sem espaços.

### 5. Status de Funil Padrão (Clean-up) 🎯
O campo principal do Zoho `Situação de Lead` está com idiomas misturados e símbolos (ex: `Meeting Scheduled / Vídeochamada Agendada`).
- **A Solução:** Extrair apenas o texto localizado em português limpo:
  - `Disqualified / Desqualificado` ➔ `Desqualificado`
  - `Meeting Scheduled / Vídeochamada Agendada` ➔ `Vídeochamada Agendada`
  - `Second Contact / 2º Contato` ➔ `2º Contato`

### 6. Tratamento de Espaços (Trim ISO)
- **A Solução:** Remover espaços inúteis no início e fim de todas as strings em todo o ficheiro, porque causam duplicações invisíveis nos filtros do Zoho CRM.

---

> [!IMPORTANT]
> **Aprovação Necessária**
> Revê as ações e indica se posso avançar com a execução ou se gostarias de alterar/adicionar alguma regra (ex: o formato do Status do funil).
