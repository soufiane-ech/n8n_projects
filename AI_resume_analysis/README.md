# AI Resume Analysis

## Description
Workflow d'automatisation n8n conçu pour traiter automatiquement les candidatures reçues par email. Il extrait les pièces jointes (CV), en analyse le contenu grâce à l'IA (LLM via OpenRouter) et consolide une évaluation structurée de chaque profil dans un tableau Google Sheets.

## Architecture du Workflow
1. **Gmail Trigger** : Surveille une boîte de réception spécifique pour les nouveaux emails.
2. **Google Drive & iLovePDF** : Télécharge le CV, le convertit si nécessaire et extrait le texte brut.
3. **OpenRouter Chat Model (Grok 4.1)** : 
   - Vérifie si le document est bien un CV.
   - Si oui, analyse le CV par rapport à une **description de poste** (stockée sur Google Drive).
   - Extrait les compétences, les forces, les faiblesses, et calcule une note d'adéquation globale.
4. **Google Sheets** : Ajoute une nouvelle ligne dans un tableau de suivi avec toutes les données extraites et l'évaluation du candidat.

## Prérequis
Pour utiliser ce workflow, vous aurez besoin des éléments suivants :
- Une instance **n8n** (version cloud ou auto-hébergée).
- Un compte **Google Cloud Console** configuré avec l'API Gmail, Google Drive et Google Sheets (authentification OAuth2).
- Un compte **iLovePDF** (pour la conversion de documents, si applicable).
- Un compte **OpenRouter** avec une clé d'API pour l'utilisation du modèle LLM (Grok 4.1 ou autre modèle performant).

## Installation et Configuration
1. **Importer le workflow** : Importez le fichier `AI Resume Analysis.json` dans votre instance n8n.
2. **Configurer les Credentials** :
   - Ajoutez et authentifiez vos credentials pour **Gmail**, **Google Drive** et **Google Sheets**.
   - Ajoutez votre clé d'API **OpenRouter**.
3. **Remplacer les Variables (Important)** :
   Dans les nœuds correspondants, remplacez les placeholders par vos propres valeurs :
   - `<VOTRE_DOSSIER_GOOGLE_DRIVE_ID>` : L'ID de votre dossier Google Drive où stocker les CV.
   - `<VOTRE_CLE_PUBLIQUE_ILOVEPDF>` : Votre clé publique iLovePDF.
   - `<VOTRE_FICHIER_DESCRIPTION_POSTE_ID>` : L'ID du fichier texte contenant la description du poste.
   - `<VOTRE_GOOGLE_SHEET_ID>` : L'ID de votre fichier Google Sheets de suivi des candidats.
4. **Fichier "description du poste.txt"** : 
   - Créez un fichier texte contenant les exigences, compétences et critères du poste visé.
   - Uploadez-le sur Google Drive et récupérez son ID pour l'étape précédente.
5. **Déployer** : Activez le workflow. Il s'exécutera automatiquement à la réception de nouveaux emails correspondants.
