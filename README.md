# U-Chat — Application de messagerie (Next.js 13 + NextAuth + Prisma / MongoDB)

![Next.js](https://img.shields.io/badge/Next.js-13-000000?logo=next.js&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript&logoColor=white)
![NextAuth](https://img.shields.io/badge/Auth-NextAuth.js-000000)
![Prisma](https://img.shields.io/badge/Prisma-MongoDB-2D3748?logo=prisma&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3-06B6D4?logo=tailwindcss&logoColor=white)
![Cloudinary](https://img.shields.io/badge/Images-Cloudinary-3448C5?logo=cloudinary&logoColor=white)

📦 **Code source** : <https://github.com/Georginio-prod/Chat>
🏠 **Landing / connexion associée** : [My-App](https://github.com/Georginio-prod/My-App)

---

## 📌 Présentation

Cœur de l'application **U-Chat** (projet du module « Mida », février–avril 2024) : une
messagerie web complète inspirée de Messenger, avec inscription, connexion sociale,
conversations individuelles et **de groupe**, envoi d'images, accusés de lecture et
paramètres de profil.

Le projet a été l'occasion d'apprendre **Next.js App Router** en profondeur, l'auth
**NextAuth** avec adaptateur Prisma et une base **MongoDB**.

## ✨ Fonctionnalités

- **Authentification** : inscription e-mail / mot de passe (`bcrypt`), connexion **GitHub** et **Google** (NextAuth), session protégée par `middleware.ts`.
- **Liste des utilisateurs** (`/users`) : démarrer une conversation en un clic.
- **Conversations** (`/conversations`) : liste des fils avec dernier message, **création de groupe** (`GroupChatModal`, sélection multiple avec `react-select`).
- **Fil de discussion** (`/conversations/[id]`) : messages texte et **images** (upload Cloudinary), affichage des avatars, **statut « vu par »** (`/seen`), suppression de conversation avec confirmation, tiroir de profil (`ProfileDrawer`) avec infos du contact / membres.
- **Paramètres** : modification du nom et de la photo de profil (`SettingsModal`).
- Interface responsive : sidebar desktop / footer mobile, états vides, modales de chargement, notifications `react-hot-toast`, données rafraîchies avec **SWR**.
- Le temps réel via Pusher est présent dans le code mais désactivé (commenté).

## 🗄️ Modèle de données (Prisma / MongoDB)

`User` (compte, mot de passe hashé, conversations, messages vus) · `Account` (OAuth) ·
`Conversation` (nom, `isGroup`, participants, messages) · `Message` (corps, image, expéditeur, `seen[]`).

## 📁 Structure

```
Chat/
├── app/
│   ├── (site)/page.tsx + compnents/AuthForm, AuthSocialButton     # Connexion / inscription
│   ├── users/                      # Liste des utilisateurs (UserList, UserBox)
│   ├── conversations/              # ConversationList, ConversationBox, GroupChatModal
│   │   └── [conversationId]/       # Header, Body, MessageBox, Form, MessageInput, ImageModal, ProfileDrawer, ConfirmModal
│   ├── api/
│   │   ├── auth/[...nextauth]/     # Providers Credentials, GitHub, Google
│   │   ├── register/ · settings/   # Inscription, mise à jour du profil
│   │   ├── conversations/ (+[id], +[id]/seen)
│   │   └── messages/
│   ├── actions/                    # getCurrentUser, getConversations, getMessages, getUsers, getSession…
│   ├── components/                 # Avatar, AvatarGroup, Button, Modal, EmptyState, Sidebar/, inputs/
│   ├── hooks/ · libs/prismadb.ts · context/ · types/
├── prisma/schema.prisma
├── middleware.ts                   # Redirection vers / si non connecté
└── tailwind.config.js
```

## 🚀 Installation & lancement

Prérequis : Node.js ≥ 18, une base **MongoDB** (Atlas), un compte Cloudinary, des apps OAuth GitHub / Google.

```bash
git clone https://github.com/Georginio-prod/Chat.git
cd Chat
npm install
```

Créer `.env` :

```dotenv
DATABASE_URL="mongodb+srv://user:password@cluster.mongodb.net/uchat"
NEXTAUTH_SECRET=une-chaine-aleatoire
GITHUB_ID=...
GITHUB_SECRET=...
GOOGLE_CLIENT_ID=...
GOOGLE_CLIENT_SECRET=...
NEXT_PUBLIC_CLOUDINARY_CLOUD_NAME=...
```

```bash
npx prisma generate
npx prisma db push
npm run dev          # http://localhost:3000
```

## 🌐 Déploiement

Non déployé : l'application nécessite MongoDB et plusieurs secrets OAuth. Elle se déploie
sur Vercel en renseignant les variables ci-dessus (et `NEXTAUTH_URL` en production).

## 🎓 Ce que ce projet démontre

Authentification complète (credentials + OAuth), modélisation de données de messagerie,
route handlers Next.js, upload de médias, UI responsive complexe (sidebar, tiroirs, modales).

---

## 👤 Auteur

**Komla Etonam Georges EKLOU** (Georginio) — Développeur Full Stack Web & Web3

[![GitHub](https://img.shields.io/badge/GitHub-Georginio--prod-181717?logo=github)](https://github.com/Georginio-prod)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Profil-0A66C2?logo=linkedin)](https://www.linkedin.com/in/komla-etonam-georges-eklou-68518b23b)
[![Portfolio](https://img.shields.io/badge/Portfolio-georginio.w3frame.com-6C63FF)](https://georginio.w3frame.com/)

> 📚 Tous mes projets sont listés et documentés sur mon [profil GitHub](https://github.com/Georginio-prod).
