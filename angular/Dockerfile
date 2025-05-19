# Etapa de build
FROM node:20.11.1-alpine as build-step

WORKDIR /app
# Copiamos los package.json
COPY package*.json ./
# Instalamos dependencias
RUN npm install
# Copiamos el resto de archivos del proyecto
COPY . .
# Compilamos Angular para producción
RUN npm run build --configuration=production && ls -la /app/dist/angular

# Etapa de producción: nginx para servir la app
FROM nginx:1.17.1-alpine
# Reemplazamos la configuración por defecto si quieres personalizar (opcional)
# COPY nginx.conf /etc/nginx/nginx.conf
# Copiamos la build generada (asegúrate del nombre de la carpeta en dist/)
COPY --from=build-step /app/dist/angular/browser /usr/share/nginx/html
