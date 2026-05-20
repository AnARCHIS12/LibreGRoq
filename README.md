<h1 align="center">LibreGRoq</h1>

<p align="center">
  <img src="https://console.groq.com/groq-logo.svg" alt="Logo Groq" width="72">
</p>

<p align="center">
  Chat Groq local, responsive, personnalisable et sauvegarde dans le navigateur.
</p>

<p align="center">
  <img alt="Groq" src="https://img.shields.io/badge/Groq-API-ef233c?style=for-the-badge">
  <img alt="Deep Chat" src="https://img.shields.io/badge/Deep%20Chat-CDN-111827?style=for-the-badge">
  <img alt="IndexedDB" src="https://img.shields.io/badge/Storage-IndexedDB-0f766e?style=for-the-badge">
  <img alt="No build" src="https://img.shields.io/badge/Build-None-38bdf8?style=for-the-badge">
  <img alt="Responsive" src="https://img.shields.io/badge/UI-Responsive-ff2bd6?style=for-the-badge">
</p>

## Aperçu

![Capture de LibreGRoq](Capture%20d%27%C3%A9cran_20260520_191755.png)

## Crédits

<p>
  Projet original de <a href="https://github.com/LaurentVoanh"><strong>LaurentVoanh</strong></a>. Merci à toi pour ce projet génial.
</p>

<p>
  <a href="https://github.com/LaurentVoanh">
    <img alt="GitHub LaurentVoanh" src="https://img.shields.io/badge/GitHub-LaurentVoanh-181717?style=for-the-badge&logo=github">
  </a>
</p>

## Fonctionnalités

- Chat avec les modèles Groq via `deep-chat`
- Configuration sauvegardée dans IndexedDB
- Historique des conversations avec recherche, renommage, épinglage et suppression
- Mémoire persistante locale, avec ajout manuel et mémoire automatique
- Profils multiples avec modèle, prompt, thème et mémoire séparés
- Thèmes simples, dont Rouge noir par défaut et Cyberpunk
- Boutons copier pour les réponses et le chat
- Export/import JSON des profils, réglages, mémoire et conversations
- Transcription audio avec `whisper-large-v3` et `whisper-large-v3-turbo`
- Nettoyage automatique des blocs `<think>...</think>`
- Interface adaptée au mobile

## Lancement

Aucune installation npm n'est nécessaire. La bibliothèque `deep-chat` est chargée par CDN.

```html
<script type="module" src="https://unpkg.com/deep-chat-dev@latest/dist/deepChat.bundle.js"></script>
```

Ouvrez `index.html` dans un navigateur, ou lancez un petit serveur local :

```bash
python3 -m http.server 4173
```

Puis ouvrez :

```text
http://localhost:4173/
```

## Configuration Groq

1. Ouvrez [console.groq.com/keys](https://console.groq.com/keys).
2. Créez une clé API.
3. Ouvrez **Réglages** dans LibreGRoq.
4. Collez la clé dans **Clé API**.
5. Choisissez le modèle, la température, le message système, le thème et la mémoire.
6. Cliquez sur **Sauvegarder**.

La clé API reste dans le navigateur avec IndexedDB. Elle n'est pas inscrite dans `index.html` et n'est pas envoyée à un serveur de cette app.

## Sauvegarde locale

LibreGRoq utilise IndexedDB avec la base `groq-chat-db`.

La sauvegarde contient :

- configuration Groq
- nom de l'app
- thème
- profils
- mémoire
- conversations
- historique de chats

Une ancienne configuration `localStorage` avec la clé `groq-chat-config` est migrée automatiquement vers IndexedDB au chargement.

## Mémoire

La mémoire est ajoutée au prompt système envoyé au modèle. Elle peut être modifiée dans les réglages, vidée, ou complétée automatiquement depuis certaines phrases utilisateur.

Exemples détectés :

- `je m'appelle Anar`
- `mon nom est Anar`
- `je préfère des réponses courtes`
- `j'habite à Paris`
- `réponds en français`

## Modèles disponibles

| Modèle | RPM | RPD | TPM | TPD |
| --- | ---: | ---: | ---: | ---: |
| llama-3.1-8b-instant | 30 | 14.4K | 6K | 500K |
| llama-3.3-70b-versatile | 30 | 1K | 12K | 100K |
| meta-llama/llama-4-scout-17b-16e-instruct | 30 | 1K | 30K | 500K |
| openai/gpt-oss-20b | 30 | 1K | 8K | 200K |
| openai/gpt-oss-120b | 30 | 1K | 8K | 200K |
| qwen/qwen3-32b | 60 | 1K | 6K | 500K |
| whisper-large-v3 | 20 | 2K | - | - |
| whisper-large-v3-turbo | 20 | 2K | - | - |
| allam-2-7b | 30 | 7K | 6K | 500K |
| groq/compound | 30 | 250 | 70K | - |
| groq/compound-mini | 30 | 250 | 70K | - |

Les limites dépendent de l'organisation Groq. Si une limite RPM ou TPM est atteinte, Groq peut retourner une erreur 429.

## Ressources

- [Documentation Groq](https://console.groq.com/docs)
- [Clés API Groq](https://console.groq.com/keys)
- [Limites Groq](https://console.groq.com/docs/rate-limits)
- [Documentation deep-chat](https://deepchat.dev/)

## Sécurité

Ne publiez jamais votre clé API dans un dépôt public. Pour un usage en production, utilisez un backend pour proxyfier les requêtes vers l'API Groq.
