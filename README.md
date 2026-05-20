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

## Apercu

![Capture de LibreGRoq](Capture%20d%27%C3%A9cran_20260520_191755.png)

## Credits

<p>
  Projet original de <a href="https://github.com/LaurentVoanh"><strong>LaurentVoanh</strong></a>. Merci a toi pour ce projet genial.
</p>

<p>
  <a href="https://github.com/LaurentVoanh">
    <img alt="GitHub LaurentVoanh" src="https://img.shields.io/badge/GitHub-LaurentVoanh-181717?style=for-the-badge&logo=github">
  </a>
</p>

## Fonctionnalites

- Chat avec les modeles Groq via `deep-chat`
- Configuration sauvegardee dans IndexedDB
- Historique des conversations avec recherche, renommage, epinglage et suppression
- Memoire persistante locale, avec ajout manuel et memoire automatique
- Profils multiples avec modele, prompt, theme et memoire separes
- Themes simples, dont Rouge noir par defaut et Cyberpunk
- Boutons copier pour les reponses et le chat
- Export/import JSON des profils, reglages, memoire et conversations
- Transcription audio avec `whisper-large-v3` et `whisper-large-v3-turbo`
- Nettoyage automatique des blocs `<think>...</think>`
- Interface adaptee au mobile

## Lancement

Aucune installation npm n'est necessaire. La bibliotheque `deep-chat` est chargee par CDN.

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
2. Creez une cle API.
3. Ouvrez **Reglages** dans LibreGRoq.
4. Collez la cle dans **Cle API**.
5. Choisissez le modele, la temperature, le message systeme, le theme et la memoire.
6. Cliquez sur **Sauvegarder**.

La cle API reste dans le navigateur avec IndexedDB. Elle n'est pas inscrite dans `index.html` et n'est pas envoyee a un serveur de cette app.

## Sauvegarde locale

LibreGRoq utilise IndexedDB avec la base `groq-chat-db`.

La sauvegarde contient :

- configuration Groq
- nom de l'app
- theme
- profils
- memoire
- conversations
- historique de chats

Une ancienne configuration `localStorage` avec la cle `groq-chat-config` est migree automatiquement vers IndexedDB au chargement.

## Memoire

La memoire est ajoutee au prompt systeme envoye au modele. Elle peut etre modifiee dans les reglages, videe, ou completee automatiquement depuis certaines phrases utilisateur.

Exemples detectes :

- `je m'appelle Anar`
- `mon nom est Anar`
- `je prefere des reponses courtes`
- `j'habite a Paris`
- `reponds en francais`

## Modeles disponibles

| Modele | RPM | RPD | TPM | TPD |
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

Les limites dependent de l'organisation Groq. Si une limite RPM ou TPM est atteinte, Groq peut retourner une erreur 429.

## Ressources

- [Documentation Groq](https://console.groq.com/docs)
- [Cles API Groq](https://console.groq.com/keys)
- [Limites Groq](https://console.groq.com/docs/rate-limits)
- [Documentation deep-chat](https://deepchat.dev/)

## Securite

Ne publiez jamais votre cle API dans un depot public. Pour un usage en production, utilisez un backend pour proxyfier les requetes vers l'API Groq.
