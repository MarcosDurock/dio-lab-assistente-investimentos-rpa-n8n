# 🤖 Assistente de Investimentos com RPA e IA no n8n

Projeto desenvolvido como parte do Desafio de Projeto da **DIO (Digital Innovation One)**, implementando uma esteira completa de hiperautomação inteligente: desde a extração de dados via Web Scraping (RPA) até a recomendação hiperpersonalizada de investimentos via LLM (OpenAI) e disparo automático via Gmail.

---

## 🎯 Objetivo da Solução

Automatizar a leitura de uma base de clientes com diferentes perfis e volumes de saldo, cruzar com as opções vigentes de produtos financeiros e gerar comunicações exclusivas, personalizadas e com rigoroso compliance financeiro, entregues diretamente na caixa de entrada dos clientes.

---

## 🏗️ Arquitetura e Fluxo de Execução

```text
[ Google Colab / Python (RPA) ]
             ↓ (POST HTTP)
      [ Túnel ngrok ]
             ↓
    [ Webhook no n8n ]
             ↓
  [ Merge (Clientes + CSV de Investimentos) ]
             ↓
[ JavaScript: Mapeamento Perfil x Produto ]
             ↓
 [ Padronização de Tabela para LLM ]
             ↓
   [ OpenAI GPT (Chat Completion) ]
             ↓
[ JavaScript: Formatação E-mail (Subject / HTML) ]
             ↓
[ Nó If: Validação Regex de E-mail (Defensiva) ]
             ↓ (True)
     [ Gmail API: Disparo Final ]
