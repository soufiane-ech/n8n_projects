# Automated Analysis of Evaluations

## Description
Workflow d'automatisation n8n pour collecter, analyser et évaluer les formulaires de satisfaction des formations de manière automatisée. Il utilise l'IA pour l'analyse de sentiment des commentaires libres et consolide toutes les données dans Google Sheets pour un suivi facile.

## Architecture du Workflow
1. **Form Trigger (n8n)** : Collecte les réponses des participants à la formation via un formulaire web natif n8n.
2. **Hugging Face API (tabularisai/multilingual-sentiment-analysis)** : Analyse le commentaire textuel laissé par le participant pour déterminer le sentiment dominant (Positif, Négatif, Neutre, etc.). Découpe automatiquement les commentaires longs.
3. **Google Sheets** : 
   - Lit un document "formateur" pour récupérer les IDs correspondants.
   - Enregistre toutes les évaluations (incluant les scores de satisfaction, logistique, contenu, et le sentiment analysé) dans un tableau récapitulatif.
4. **Logique métier (Python)** : Transforme et formate les données extraites, gère le mapping des IDs de formation et génère des identifiants uniques pour chaque évaluation.

## Prérequis
Pour utiliser ce workflow, vous aurez besoin des éléments suivants :
- Une instance **n8n** (version cloud ou auto-hébergée).
- Un compte **Google Cloud Console** configuré avec l'API Google Sheets (authentification OAuth2).
- Un compte **Hugging Face** avec un Access Token pour utiliser l'API d'inférence.

## Installation et Configuration
1. **Importer le workflow** : Importez le fichier `Automated_Analysis_of_Evaluations.json` dans votre instance n8n.
2. **Configurer les Credentials** :
   - Ajoutez et authentifiez vos credentials pour **Google Sheets**.
3. **Remplacer les Variables (Important)** :
   Dans les nœuds "HTTP Request" et "Google Sheets", remplacez les placeholders par vos propres valeurs :
   - `<VOTRE_TOKEN_HUGGING_FACE>` : Votre jeton d'accès Hugging Face (dans les nœuds d'analyse de sentiment).
   - `<VOTRE_GOOGLE_SHEET_ID_FORMATEUR>` : L'ID de la feuille Google Sheets contenant la base de données des formateurs.
   - `<VOTRE_GOOGLE_SHEET_ID_TEST>` : L'ID de la feuille Google Sheets où seront stockées les évaluations (dans les nœuds de sauvegarde et de lecture).
4. **Déployer** : 
   - Activez le workflow. 
   - Récupérez l'URL du formulaire générée par le nœud "Form Trigger" et partagez-la avec les participants.

