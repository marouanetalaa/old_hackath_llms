# RAG pour la Santé

Ce projet démontre l’utilisation de la technique **Retrieval-Augmented Generation (RAG)** pour répondre de manière plus pertinente à un benchmark médical à l’aide d’un Large Language Model (LLM). L’approche consiste à constituer une base de connaissances spécifique et à intégrer, en temps réel, les extraits les plus pertinents dans le prompt du LLM.

---

## Contexte

- **Objectif :** Améliorer la pertinence des réponses générées par un LLM dans un contexte de **données médicales**.  
- **Problématique :** Les modèles de langage génériques peinent souvent à fournir des réponses précises sur des sujets spécialisés (ici, la santé).  
- **Solution :** Incorporer un moteur de recherche vectoriel pour retrouver des extraits ciblés (articles, études médicales, etc.) et les inclure directement dans les requêtes soumises au LLM.

## Architecture du projet

1. **Base de connaissances** : Ensemble de documents médicaux (articles, études, publications, guidelines…) organisés et indexés.  
2. **Moteur de recherche vectoriel** :  
   - Calcul des embeddings de chaque document (ou paragraphe) pour un accès rapide par similarité.  
   - Recherche des passages les plus pertinents en fonction de la requête utilisateur.  
3. **Pipeline RAG** :  
   - Requête utilisateur → Embedding → Similarité → Extraction des top-k passages → Construction du prompt → Envoi au LLM → Réponse augmentée.  

Le schéma simplifié :

```
┌───────────────┐      ┌─────────────────────────┐      ┌─────────────────────┐
│ Requête        │      │ Moteur de recherche     │      │ LLM (Language Model)│
│ utilisateur    ├─────→│ (Vectoriel)             ├─────→│ + Contexte          │
└───────────────┘      └─────────────────────────┘      └─────────────────────┘
                            ↑
                            │   Base de
                            │   connaissances
                            │
                        (articles, études)
```

## Dépendances

- **Langages** : Python (3.8+ recommandé)  
- **Bibliothèques** :  
  - [Transformers](https://github.com/huggingface/transformers) pour le LLM  
  - [Sentence-Transformers](https://github.com/UKPLab/sentence-transformers) pour la vectorisation  
  - [faiss-cpu](https://github.com/facebookresearch/faiss) (ou autre vectordb) pour la recherche  
  - [pandas](https://pandas.pydata.org/) pour la gestion des données  


