# 📝 Padronização de Notas e Registo de Eventos

Após varrer as 69 colunas da base atual, identifiquei **2 campos principais** que contêm informações longas em formato de texto livre ou logs de sistema, e propunho a seguinte padronização para tornar a leitura muito mais intuitiva para a tua equipa no Zoho:

## 1. Notas Humanas: Campo `Descrição` (3.354 leads)
Este campo contém as verdadeiras notas deixadas pelos SDRs ou vendedores (ex: *"Sem WhatsApp, mandei e-mail..."* ou *"Informou que já fez avaliação no Brasil..."*).
**Ação Proposta:**
- Renomear a coluna de `Descrição` para `Notas da Equipa` (mais claro para CRM).
- Aplicar limpeza de formatação (remover quebras de linha múltiplas e espaços extra).

## 2. Logs de Sistema: Campo `Eventos (Últimos 100)` (21.660 leads)
Este campo é um despejo automático do RD Station e é impossível ler à primeira vista (ex: *"Tarefa criada no RD Station CRM / Negociação atualizada no RD Station... "*). É apenas ruído se deixado assim.
**Ação Proposta: Criar 2 novas colunas inteligentes:**
- **Coluna A (`Total de Interações Sistema`):** Contar automaticamente quantos eventos ocorreram com este lead. Isto vai gerar um número (ex: `15`), ajudando a equipa a ver se é um lead muito ou pouco "tocado" pelo marketing.
- **Coluna B (`Último Evento Registado`):** Extrair apenas a primeira/última ação desse bloco de texto gigante, para sabermos qual foi o último gatilho exato do lead antes de chegar a esta tabela, ignorando o resto.
- Após extrair estas 2 informações úteis, podemos **remover** a coluna gigante original `Eventos...` para despoluir o Excel.

---
> [!IMPORTANT]  
> Posso avançar com esta limpeza e resumo estruturado das notas para gerar um ficheiro ainda melhor?
