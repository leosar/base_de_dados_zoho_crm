# 🎯 Modelo de 'Lead Scoring' e Propensão de Compra (B2C Clínico)

Com base nas melhores práticas do mercado de *Predictive Lead Scoring* e *Propensity-to-Buy Models* (especialmente focado no setor de saúde B2C: Dental/Médico), os leads devem ser avaliados com base em **Dados Explícitos** (perfil) e **Dados Implícitos** (comportamento e intenção).

Para a base de 31.000+ leads que acabámos de limpar, proponho a criação de **duas novas colunas**: `Score de Conversão (0-100)` e `Rank do Lead (A, B, C)`.

O algoritmo vai analisar cada lead e calcular a nota da seguinte forma:

## 📊 A. Sistema de Pontuação (Peso de 100 Pontos)

### 1. Integridade de Contato (Máx: 20 pts)
Um lead só tem probabilidade real de converter se a clínica conseguir falar com ele.
- **+10 pts:** Tem `Celular` válido (norma E.164).
- **+5 pts:** Tem `E-mail` válido.
- **+5 pts:** Tem `País` / `Cidade` preenchidos (permite segmentar se está na área de alcance).

### 2. Comportamento e Engajamento (Máx: 40 pts)
Aproveitamos o campo limpo das interações automáticas do sistema.
- **Interações do Sistema (RD Station / Automação):**
  - **+20 pts:** Mais de 10 interações. *(Lead altamente engajado e a consumir conteúdo)*.
  - **+10 pts:** 4 a 10 interações. *(Interesse médio)*.
  - **+5 pts:** 1 a 3 interações. *(Topo de funil)*.
- **Sinais Manuais Antigos (se preenchidos):**
  - **+10 pts:** Se a coluna `SDR Score` original for alta ou `Lead Priority` for "A" ou "High" (onde as equipas no passado deixaram já sinalizado).
  - **+10 pts:** Se "Vídeochamada Confirmada" for True nalgum momento do histórico.

### 3. Intenção no Funil de Vendas (Máx: 40 pts)
O ponto fundamental: o quão perto do ato médico ou agendamento o lead esteve. Analisado pela coluna `Situação de Lead`.
- **+40 pts:** `Vídeochamada Agendada` / `Meeting Confirmed` *(Intenção Máxima)*.
- **+20 pts:** `2º Contato` / `3º Contato` *(O SDR já teve trabalho aqui)*.
- **+10 pts:** `1º Contato` / `Pré-qualificado` / `Novo Lead`.
- **+5 pts:** `Nutrição` / `Cursos` *(Interessado, mas frio)*.

### ⚠️ Penalizações Severas (Negative Scoring)
As boas práticas ditam que devemos retirar pontos agressivamente a quem já provou não ter fit:
- **-50 pts:** Status `Desqualificado` *(Lead morto, cai imediatamente para o fim da lista)*.
- **-30 pts:** Status `No-Show` *(Faltou à consulta/vídeo, intenção duvidosa)*.
- **-10 pts:** Status `Repescagem` *(Esfriou e voltou, perdeu o timing principal)*.

---

## 🏆 B. Hierarquia de Ranks Automática

Após somar todos os pontos, a pontuação final será "cortada" entre 0 e 100, gerando um rank muito visual para as vendas:

| Rank | Pontuação (Score) | Probabilidade de Fecho | Ação Recomendada para o SDR |
|---|---|---|---|
| 🔥 **A (Quente)** | **75 a 100 pts** | Altíssima | Ligar imediatamente. São os "Low Hanging Fruits". |
| 🟡 **B (Morno)** | **40 a 74 pts** | Média | Enviar SMS ou mensagem no WhatsApp. Precisam de aquecimento. |
| 🧊 **C (Frio)** | **0 a 39 pts** | Baixa / Nula | Deixar na automação de E-mail Marketing. Não gastar tempo humano. |

---

> [!CAUTION]
> **Aprovação Necessária:** Revê por favor a lógica de pontuação acima. Faz sentido para o dia a dia da clínica? Posso avançar com a execução do script para aplicar de imediato na base de dados?
