# n8n Automation Projects Showcase

Ce dépôt rassemble une collection de workflows d'automatisation **n8n** professionnels, prêts à être déployés. Ils illustrent comment combiner l'orchestration de données, le scraping, l'intelligence artificielle et les outils de productivité (Google Workspace, APIs externes) pour répondre à des cas d'usage métiers concrets.

## Projets inclus

### 1. [AI Resume Analysis](./AI_resume_analysis/)
Un pipeline automatisé pour les ressources humaines. 
- **Objectif** : Évaluer automatiquement les candidatures reçues par email.
- **Fonctionnement** : Extrait les CV en pièces jointes, les convertit en texte, puis utilise un Modèle de Langage (LLM via OpenRouter) pour évaluer l'adéquation du profil par rapport à une description de poste. Les résultats sont centralisés dans Google Sheets.

### 2. [Automated Analysis of Evaluations](./Automated_Analysis_of_Evaluations/)
Une solution d'analyse de formulaires de satisfaction pour les formations.
- **Objectif** : Collecter et analyser intelligemment les retours de formation.
- **Fonctionnement** : Capture les données soumises via un formulaire n8n, analyse le sentiment des commentaires libres avec Hugging Face, attribue des identifiants de formateurs, et enregistre un récapitulatif détaillé dans une base de données Google Sheets.

### 3. [Product Reviews Sentiment Analysis](./product_reviews_sentiment_analysis/)
Un outil de veille concurrentielle et de réputation e-commerce.
- **Objectif** : Scraper et analyser les avis clients sur Amazon.
- **Fonctionnement** : Déclenché par l'envoi d'une URL produit via chat, le workflow utilise Apify pour scraper les avis, puis analyse finement les sentiments de chaque commentaire via Hugging Face. Les statistiques consolidées sont exportées sur Google Sheets.

