# Usa la imagen base oficial de Node
FROM node:20-alpine

# Definir el directorio de trabajo
WORKDIR /app

# Copiar los archivos package.json y package-lock.json
COPY package*.json ./

# Instalar las dependencias de npm
RUN npm install

# Copiar todo el contenido de la carpeta frontend
COPY . .

# Exponer el puerto 5173 (que es el puerto por defecto de Vite)
EXPOSE 5173

# Comando por defecto para ejecutar la app con Vite
CMD ["npm", "run", "dev"]
