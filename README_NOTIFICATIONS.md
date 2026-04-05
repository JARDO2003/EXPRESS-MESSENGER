# GE Messenger - Système de Notifications Complet

## 🔔 Nouvelles Fonctionnalités de Notification

### 1. Notifications en Arrière-Plan (Même PWA Fermée)
- Les notifications fonctionnent même lorsque l'utilisateur a fermé la PWA
- Utilisation de Firebase Cloud Messaging (FCM) pour les push notifications
- Service Worker gère les notifications en arrière-plan

### 2. Système de "Vu" (Deux Traits WhatsApp)
- **✓** = Message envoyé (sent)
- **✓✓** = Message livré (delivered)  
- **✓✓ (bleu)** = Message lu (read)
- Affichage en temps réel du statut de lecture

### 3. Compteurs de Messages Non Lus
- Badge sur les conversations avec messages non lus
- Compteur sur l'icône Messages dans la navigation
- Mise en évidence visuelle des conversations non lues (fond rougeâtre)

### 4. Notifications pour Nouvelles Publications
- Notification quand un contact publie quelque chose
- Badge sur l'onglet "Actu" avec le nombre de nouvelles publications
- Son et vibration configurables

### 5. Notifications pour Likes
- Notification quand quelqu'un aime votre publication
- Son discret avec vibration légère

### 6. Bannière "Nouveaux Messages" (Style WhatsApp)
- Apparaît quand de nouveaux messages arrivent et que l'utilisateur n'est pas en bas de la conversation
- Compteur de messages non lus dans la conversation active
- Clique pour scroll vers le bas

### 7. Types de Notifications Supportés
- 💬 **Messages** - Avec actions: Répondre, Lu, Ignorer
- 📰 **Publications** - Avec actions: Voir, J'aime, Ignorer
- ❤️ **Likes** - Avec actions: Voir, Ignorer
- 📞 **Appels** - Avec actions: Répondre, Refuser
- ✨ **Stories** - Avec actions: Voir, Répondre, Ignorer

## 📁 Fichiers Modifiés/Créés

### `firebase-messaging-sw.js`
Service Worker complet avec:
- Gestion des notifications en arrière-plan
- Différents types de notifications
- Actions sur les notifications (reply, read, like, etc.)
- Vibration patterns par type
- Gestion des clics sur notifications

### `index.html`
Application principale avec:
- Système de read receipts (deux traits)
- Compteurs de messages non lus
- Bannière de nouveaux messages
- Gestion des notifications en temps réel
- Panel de configuration des notifications

### `sender.js`
Serveur de notifications avec:
- Envoi multicast FCM
- Gestion des tokens invalides
- Différents types de messages
- Construction dynamique des notifications

## ⚙️ Configuration des Notifications

Le panel de notifications permet de configurer:
- ✅ Activer/Désactiver toutes les notifications
- 📳 Activer/Désactiver la vibration
- 💬 Notifications de messages
- 📞 Notifications d'appels
- 📰 Notifications de publications
- ❤️ Notifications de likes
- 🔊 Volume des sons
- 🎵 Son des messages
- 🎵 Son des appels

## 🔧 Fonctionnement Technique

### Flux de Notification Message
1. Utilisateur A envoie un message
2. Message sauvegardé dans Firestore
3. Notification créée dans `ge_notifications`
4. Si destinataire a FCM token → Push notification envoyée
5. Service Worker affiche la notification
6. Si app ouverte → Son + vibration + toast

### Système de Read Receipts
1. Message envoyé → Status: `sent`
2. Message livré au destinataire → Status: `delivered`
3. Destinataire ouvre la conversation → Status: `read`
4. Affichage visuel avec icônes ✓ / ✓✓ / ✓✓(bleu)

### Compteurs Non Lus
1. Chaque message a un tableau `readBy`
2. Si l'utilisateur n'est pas dans `readBy` → compteur +1
3. Quand conversation ouverte → marquer tous comme lus
4. Mise à jour en temps réel avec onSnapshot

## 🚀 Déploiement

```bash
# Installer les dépendances
npm install

# Déployer sur Vercel
vercel --prod
```

## 📱 Test des Notifications

1. Ouvrir le panel de notifications (🔔)
2. Cliquer sur "Activer" pour demander la permission
3. Autoriser les notifications dans le navigateur
4. Utiliser "Tester tous les sons" pour vérifier

## 🔒 Sécurité

- Les tokens FCM sont stockés dans Firestore
- Suppression automatique des tokens invalides
- Notifications chiffrées via HTTPS/FCM
