# Product Reviews Sentiment Analysis

## Description
Workflow d'automatisation n8n conçu pour scraper automatiquement les avis de produits Amazon et analyser en profondeur le sentiment de chaque commentaire à l'aide de l'Intelligence Artificielle. Idéal pour la veille concurrentielle et le suivi de réputation.

## Architecture du Workflow
1. **Chat Trigger (n8n)** : Déclenche le workflow à la réception d'un message (contenant l'URL du produit Amazon).
2. **Extraction de l'ASIN (Python)** : Isole l'identifiant unique du produit (ASIN) à partir de l'URL fournie.
3. **Apify (amazon-reviews-scraper)** : Exécute un scraping externe sur Amazon pour récupérer les avis pertinents, leurs notes et dates.
4. **Hugging Face API (tabularisai/multilingual-sentiment-analysis)** : 
   - Analyse le texte de chaque avis. 
   - Les avis trop longs sont automatiquement découpés en plusieurs parties.
   - Attribue des scores de confiance sur 5 émotions : Très Positif, Positif, Neutre, Négatif, Très Négatif.
5. **Agrégration et Google Sheets** :
   - Calcule la moyenne des sentiments pour l'ensemble du produit.
   - Sauvegarde les avis bruts, les avis analysés, et le résumé global des sentiments dans différentes feuilles d'un document Google Sheets.

## Prérequis
Pour utiliser ce workflow, vous aurez besoin des éléments suivants :
- Une instance **n8n** (version cloud ou auto-hébergée).
- Un compte **Apify** avec l'Actor `axesso_data/amazon-reviews-scraper` prêt à être utilisé.
- Un compte **Hugging Face** avec un Access Token pour l'analyse de sentiment.
- Un compte **Google Cloud Console** configuré avec l'API Google Sheets (authentification OAuth2).

## Installation et Configuration
1. **Importer le workflow** : Importez le fichier `Product Reviews Sentiment Analysis.json` dans votre instance n8n.
2. **Configurer les Credentials** :
   - Ajoutez et authentifiez vos credentials pour **Google Sheets** et **Apify**.
3. **Remplacer les Variables (Important)** :
   Vérifiez les nœuds du workflow et remplacez les placeholders par vos valeurs :
   - `<VOTRE_TOKEN_HUGGING_FACE>` : Votre jeton d'accès personnel Hugging Face.
   - `<VOTRE_GOOGLE_SHEET_ID>` : L'ID de votre classeur Google Sheets (qui doit contenir au moins 3 onglets distincts pour le brut, l'analyse et le résumé).
4. **Déployer** : 
   - Activez le workflow. 
   - Ouvrez l'interface de Chat intégrée à n8n et envoyez l'URL d'un produit Amazon pour lancer l'analyse.

