# 🔍 Análise da Base de Leads — CRM Zoho

**Ficheiro:** `Leads_2026_03_23.xlsx`  
**Data da análise:** 2026-03-23  
**Total de leads:** 31.774 | **Total de colunas:** 172

---

## 📊 Resumo Executivo

A base de leads tem **sérios problemas de organização** que precisam ser resolvidos:

| Problema | Quantidade | Impacto |
|---|---|---|
| Colunas 100% vazias (0 dados) | **42 colunas** | 🔴 Crítico — lixo puro |
| Colunas quase vazias (<1%) | **~30 colunas** | 🟠 Alto — ruído desnecessário |
| Colunas com valor constante (inúteis) | **7 colunas** | 🔴 Crítico — zero informação |
| Campos duplicados/redundantes | **5 pares** | 🟠 Alto — dados fragmentados |
| Formatações inconsistentes | **4 campos críticos** | 🟡 Médio — dificulta filtros e relatórios |
| Leads com nomes duplicados | **4.791** | 🟡 Médio — possíveis duplicatas |
| E-mails duplicados | **115** | 🟡 Médio — leads potencialmente repetidos |

> [!CAUTION]
> Das 172 colunas, **pelo menos 80 podem ser removidas** sem perda de informação útil. Isso significa que quase **metade da base é lixo**.

---

## 🔴 1. Colunas 100% Vazias — Remover Imediatamente

Estas 42 colunas não têm **nenhum dado**. São campos que nunca foram preenchidos:

| # | Coluna | Observação |
|---|---|---|
| 1 | `Data/Hora convertidas` | Nunca houve conversão (todos são "False") |
| 2 | `Lead Tempo de conversão` | Idem |
| 3 | `Modo do cancelamento de inscrição` | Nunca usado |
| 4 | `Horário do cancelamento de inscrição` | Nunca usado |
| 5 | `Contato convertido.id` | Sem conversões |
| 6 | `Contato convertido` | Sem conversões |
| 7 | `Negócio convertido.id` | Sem conversões |
| 8 | `Negócio convertido` | Sem conversões |
| 9 | `Horário do último enriquecimento` | Enriquecimento nunca usado |
| 10 | `Enriquecer status` | Idem |
| 11 | `Número do Documento` | Nunca preenchido |
| 12 | `IBAN` | Nunca preenchido |
| 13 | `Reportando-se a.id` | Sem uso |
| 14 | `Reportando-se a` | Sem uso |
| 15 | `Departamento` | Sem uso |
| 16 | `GCLID` | Google Ads — nunca integrado |
| 17 | `ID DA CAMPANHA Z` | Nunca preenchido |
| 18 | `ADGROUPID` | Nunca preenchido |
| 19 | `ADID` | Nunca preenchido |
| 20 | `KEYWORDID` | Nunca preenchido |
| 21 | `Palavra-chave` | Nunca preenchido |
| 22 | `Clique em tipo` | Nunca preenchido |
| 23 | `Tipo de dispositivo` | Nunca preenchido |
| 24 | `Rede de anúncios` | Nunca preenchido |
| 25 | `Pesquisar rede de parceiros` | Nunca preenchido |
| 26 | `Nome da campanha do anúncio` | Nunca preenchido |
| 27 | `Nome do grupos de anúncios` | Nunca preenchido |
| 28 | `Anúncio` | Nunca preenchido |
| 29 | `GADCONFIGID` | Nunca preenchido |
| 30 | `Ad Click Date` | Nunca preenchido |
| 31 | `Conversion Exported On` | Nunca preenchido |
| 32 | `Conversion Export Status` | Nunca preenchido |
| 33 | `Reason for Conversion Failure` | Nunca preenchido |
| 34 | `Linkedin` | Nunca preenchido |
| 35 | `Facebook` | Nunca preenchido |
| 36 | `X (Twitter)` | Nunca preenchido |
| 37 | `Qual seu principal desafio com alimentação?` | Nunca preenchido |
| 38 | `Notas Transcritas` | Nunca preenchido |
| 39 | `Connected To.module` | Nunca preenchido |
| 40 | `Origem (Plataforma)` | Nunca preenchido |
| 41 | `Fonte  (LP)` | Nunca preenchido |
| 42 | `Palavra chave` | Nunca preenchido (duplica "Palavra-chave") |

> Também 100% vazias: `Meta Event ID`, `NÃO PREENCHER OS CAMPOS ABAIXO DESSA SEÇÃO`, `FAVOR NÃO PREENCHER OS CAMPOS ABAIXO DESSA SEÇÃO` — colunas "fantasma" que servem de separador visual no Zoho mas não têm dados.

---

## 🔴 2. Colunas com Valor Constante — Remover

Estas colunas estão 100% preenchidas mas com o **mesmo valor em todos os 31.774 leads**:

| Coluna | Valor em TODAS as linhas |
|---|---|
| `Está convertido` | `False` (nenhum lead convertido) |
| `Opção de Sair do E-mail` | `False` |
| `Locked` | `False` |
| `Cost per Click` | `0` |
| `Cost per Conversion` | `0` |
| `Confirmar Agendamento` | `False` |

> [!NOTE]
> Estas colunas não acrescentam informação porque o valor nunca varia. São ruído.

---

## 🟠 3. Campos Duplicados e Redundantes — Unificar

Existem **5 pares de campos** que guardam a mesma informação de formas diferentes:

| Campo A | Preenchido | Campo B | Preenchido | Ação |
|---|---|---|---|---|
| `Proprietário do Lead` | 31.772 (100%) | `Dono do Lead` | 17.919 (56%) | Manter apenas `Proprietário do Lead` |
| `Agendamento Video` | 242 | `Agendamento vídeo.` | 8 | Fundir em `Agendamento Video` |
| `Palavra-chave` | 0 | `Palavra chave` | 0 | Remover ambas (vazias) |
| `Cidade` | 15.070 (47%) | `QUAL SUA CIDADE?` | 1.407 (4%) | Fundir tudo em `Cidade` |
| `País` | 3.418 (11%) | `Em que país você mora?` + `PAÍS ALTERNATIVO` | 402 + 107 | Fundir tudo em `País` |

> [!IMPORTANT]
> Os dados duplicados de cidade e país devem ser **fundidos antes de remover** as colunas alternativas — caso contrário perde-se informação!

---

## 🟡 4. Formatações Inconsistentes

### 4.1 País — Caos total 🌍

O mesmo país aparece escrito de **múltiplas formas**:

| País Real | Variações encontradas |
|---|---|
| 🇫🇷 França | `França`, `FR`, `France` |
| 🇵🇹 Portugal | `PT` |
| 🇧🇪 Bélgica | `Bélgica`, `BE` |
| 🇨🇭 Suíça | `Suiça`, `CH` |
| 🇬🇧 Reino Unido | `GB` |
| 🇱🇺 Luxemburgo | `Luxemburgo`, `Luxenburgo` (typo!), `LU` |
| 🇳🇱 Holanda | `NL` |
| 🇩🇪 Alemanha | `DE` |
| 🇧🇷 Brasil | `BR` |
| 🇺🇸 EUA | `US` |

**Ação:** Padronizar para nome completo em português OU código ISO (escolher um).

### 4.2 Fonte de Lead — Duplicações claras 📢

| Fonte | Registos | É a mesma coisa? |
|---|---|---|
| `LP-D` | 2.932 | ✅ Sim |
| `LP - D` | 882 | ✅ Mesmo que `LP-D` |
| `MetaADS` | 2.753 | ✅ Sim |
| `Meta ADS` | 2.609 | ✅ Mesmo que `MetaADS` |

**Ação:** Padronizar para `LP-D` e `Meta ADS` (ou outro padrão).

### 4.3 Interesses — Variações do mesmo produto 🦷

| Interesse Real | Variações |
|---|---|
| Implantes Dentários | `Implantes Dentários` (11.256), `implantes` (2.142), `Implantes` (1.960), `Implante Dentários` (489), `implante` (472), `[DIEGO] Implantes` (313) |
| Facetas | `Facetas` (1.002), `facetas 36x` (50) |
| Alinhadores | `Alinhadores` (1.125), `[DIEGO] Alinhadores` (65) |
| Transplante Capilar | `Transplante Capilar` (712), `[diego] trans. capilar` (81) |

**Ação:** Normalizar para categorias únicas e remover prefixos como `[DIEGO]`, `[wb]`.

### 4.4 Telefones (Celular) — Formato misto 📱

Dos 4.231 telefones preenchidos:

| Formato | Quantidade |
|---|---|
| Com `+` (ex: `+32465325503`) | 3.336 (79%) |
| Só dígitos sem `+` (ex: `351911896027`) | 893 (21%) |
| Com espaços | 37 |
| Com traços | 3 |

**Ação:** Padronizar todos para formato internacional com `+` (ex: `+351911896027`).

---

## 🟠 5. Colunas Quase Vazias — Avaliar Remoção

Estas colunas têm **menos de 1% de preenchimento** (<318 registos em 31.774):

| Coluna | Preenchidos | % | Decisão sugerida |
|---|---|---|---|
| `Saudação` | 46 | 0.1% | ❌ Remover |
| `E-mail secundário` | 14 | 0.0% | ❌ Remover |
| `Social Lead ID` | 1 | 0.0% | ❌ Remover |
| `Data de Nascimento` | 6 | 0.0% | ❌ Remover |
| `Doutor Responsável` | 12 | 0.0% | ❌ Remover |
| `Morada` | 7 | 0.0% | ❌ Remover |
| `Documento de Identificação` | 2 | 0.0% | ❌ Remover |
| `NIF` | 5 | 0.0% | ❌ Remover |
| `Data de aniversário` | 1 | 0.0% | ❌ Remover |
| `Notas NoviGest` | 2 | 0.0% | ❌ Remover |
| `ID Zoho` | 13 | 0.0% | ❌ Remover |
| `Agendamento vídeo.` | 8 | 0.0% | ❌ Fundir com `Agendamento Video` |
| `Previous Investment` | 9 | 0.0% | ❌ Remover |
| `Website (RdStation)` | 81 | 0.3% | ⚠️ Avaliar |
| `Qual serviço você está buscando?` | 28 | 0.1% | ❌ Remover |
| `Biografia` | 48 | 0.2% | ❌ Remover |
| `QUAL O HORÁRIO DE CONTATO?` | 54 | 0.2% | ❌ Remover |
| `Código Novigest` | 34 | 0.1% | ⚠️ Avaliar (pode ser útil para integração) |
| `Budget Range` | 17 | 0.1% | ❌ Remover |
| `Travel Planned` | 21 | 0.1% | ❌ Remover |
| `Payment Preference` | 18 | 0.1% | ❌ Remover |
| `Expat Location` | 17 | 0.1% | ❌ Remover |

---

## 🟠 6. Colunas de Sistema/Técnicas — Considerar Ocultar

Estas colunas são IDs internos do sistema que não têm valor para análise de negócio:

| Coluna | Observação |
|---|---|
| `ID do registro` | ID interno Zoho — manter como chave mas ocultar |
| `Proprietário do Lead.id` | ID interno — manter só o nome |
| `Criado Por.id` | ID interno |
| `Modificado Por.id` | ID interno |
| `Layout.id` | ID interno |
| `Contato convertido.id` | Vazio + ID interno |
| `Negócio convertido.id` | Vazio + ID interno |
| `Conectado a.id` | Vazio + ID interno |
| `Responsible Closer.id` | ID interno |
| `Closer ID` | Duplica Responsible Closer |

---

## 📋 7. Potenciais Leads Duplicados

| Tipo | Quantidade | Observação |
|---|---|---|
| Nomes duplicados | 4.791 leads | Podem ser pessoas diferentes com mesmo nome |
| E-mails duplicados | 115 leads | **Muito provavelmente duplicatas reais** |
| Telefones duplicados | 24 leads | Provavelmente duplicatas |

**Ação:** Investigar e fundir os 115 leads com e-mail duplicado.

---

## ✅ Plano de Ação Priorizado

### Fase 1 — Limpeza Imediata (sem risco)
1. ❌ Remover as **42 colunas 100% vazias**
2. ❌ Remover as **7 colunas de valor constante**
3. ❌ Remover as **~20 colunas com <0.5% preenchimento**
4. ❌ Remover colunas "separadoras" (`NÃO PREENCHER...`)

### Fase 2 — Unificação de Campos
5. 🔀 Fundir `Dono do Lead` → `Proprietário do Lead`
6. 🔀 Fundir `QUAL SUA CIDADE?` → `Cidade`
7. 🔀 Fundir `Em que país você mora?` + `PAÍS ALTERNATIVO` → `País`
8. 🔀 Fundir `Agendamento vídeo.` → `Agendamento Video`

### Fase 3 — Padronização de Dados
9. 🔧 Padronizar nomes de países (ISO ou nome completo)
10. 🔧 Padronizar `Fonte de Lead` (`LP-D`/`LP - D`, `MetaADS`/`Meta ADS`)
11. 🔧 Padronizar `Interesses` (unificar variantes, remover prefixos)
12. 🔧 Padronizar `Celular` para formato `+XXX...`

### Fase 4 — Deduplicação
13. 🔍 Investigar e tratar 115 leads com e-mail duplicado
14. 🔍 Revisar 24 leads com telefone duplicado

### Resultado Esperado
- De **172 colunas** → ~**70-80 colunas** úteis e organizadas
- Dados padronizados e filtráveis
- Eliminação de duplicatas confirmadas
