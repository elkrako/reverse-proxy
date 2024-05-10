# Étape 1: Construire l'image basée sur l'image officielle Node.js
FROM node:16-alpine as build

# Définir le répertoire de travail dans le conteneur
WORKDIR /app

# Copier les fichiers package.json et package-lock.json (ou yarn.lock)
COPY package*.json ./

# Installer les dépendances
RUN npm install

# Copier le reste des fichiers du projet
COPY . .

# Construire l'application Nuxt
RUN npm run build

# Étape 2: Préparer l'image de production avec Nginx
FROM nginx:alpine

# Copier le build de Nuxt dans le répertoire de service de Nginx
COPY --from=build /app/.nuxt/dist/client /usr/share/nginx/html

# Copier une configuration Nginx spécifique si nécessaire
# COPY nginx.conf /etc/nginx/nginx.conf

# Exposer le port (Nginx écoute sur le port 80 par défaut)
EXPOSE 80

# Commande pour démarrer Nginx dans le conteneur
CMD ["nginx", "-g", "daemon off;"]
