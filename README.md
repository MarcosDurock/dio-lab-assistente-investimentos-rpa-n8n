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

----

🧠 Decisões Técnicas e Boas Práticas
1. RPA com BeautifulSoup e Requisição Webhook
Por quê? A extração tabular com BeautifulSoup permitiu tratar e limpar os dados de clientes diretamente da página web estática, encapsulando-os em um payload JSON limpo enviado via requests.post.

2. Túnel Seguro com ngrok
Por quê? Como o n8n está hospedado localmente via Docker (em localhost:5678) e o Google Colab roda na nuvem do Google, o ngrok criou um endpoint público seguro para rotear o webhook sem necessidade de expor portas do roteador.

3. Mapeamento Defensivo e Normalização de Dados (JavaScript)
Por quê? No nó Code, foi aplicada normalização de strings numéricas (Regex /[^\d]/g) e tratamento com operadores de coalescência nula (??) e fallback seguro, garantindo que clientes sem investimento direto recebam uma recomendação padrão sem quebrar a execução.

4. Engenharia de Prompt e Compliance Financeiro (LLM)
Por quê? Em conformidade com regras regulatórias (CVM/Anbima), o prompt instrui a OpenAI a adotar tom consultivo, acolhedor e conciso (pt-BR), proibindo explicitamente garantias de rentabilidade ou promessas de ganhos futuros, tratando valores apenas como estimativas de mercado.

5. Programação Defensiva com Regex no E-mail
Por quê? Um nó If com a expressão regular ^[^\s@]+@[^\s@]+\.[^\s@]+$ valida os endereços antes do nó do Gmail. Se algum registro contiver e-mail inválido ou nulo, ele é isolado no branch False, evitando erros de execução e garantindo que o lote continue sendo processado.

6. Autenticação OAuth2 Google Cloud
Por quê? Implementação de credenciais oficiais via Google Cloud Console com escopos restritos da Gmail API, garantindo segurança na autenticação e envio de mensagens.
🛠️ Tecnologias Utilizadas
n8n (Orquestração e Workflows)
Docker & Docker Compose (Containerização do ambiente)
Python (Requests + BeautifulSoup) (RPA e Scraping)
OpenAI API (GPT) (Geração de texto personalizada)
Gmail API (Disparo de e-mails via OAuth2)
ngrok (Túnel reverso para Webhook)

📹 Demonstração do Projeto
Vídeo demonstrativo: Assista ao vídeo no Google Drive
