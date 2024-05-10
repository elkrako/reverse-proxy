# Node image
FROM node:16-alpine as build

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build


# Nginx image
FROM nginx:alpine

# Copier le build de Nuxt dans le répertoire de service de Nginx
COPY --from=build /app/.nuxt/dist/client /usr/share/nginx/html

# Copier une configuration Nginx spécifique si nécessaire
# COPY nginx.conf /etc/nginx/nginx.conf

# Exposer le port (Nginx écoute sur le port 80 par défaut)
EXPOSE 80

# Commande pour démarrer Nginx dans le conteneur
CMD ["nginx", "-g", "daemon off;"]
