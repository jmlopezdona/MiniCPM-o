# Usar la imagen oficial de Node.js 18 como base
# To build image: docker build -t minicpm-o_2.6-webapp:latest .
# To run container: docker run -it --rm -p 8088:8088 minicpm-o_2.6-webapp:latest
FROM node:18

# Clonar el repositorio de MiniCPM-o
RUN git clone https://github.com/jmlopezdona/MiniCPM-o.git /app/MiniCPM-o

# Cambiar al directorio del proyecto
WORKDIR /app/MiniCPM-o

# Instalar PNPM globalmente
RUN npm install -g pnpm

# Cambiar al directorio del servidor web
WORKDIR /app/MiniCPM-o/web_demos/minicpm-o_2.6/web_server

# Crear un certificado SSL autofirmado sin interacción
RUN openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365 -nodes \
    -subj "/C=ES/ST=Madrid/L=Madrid/O=MyDevOrg/OU=Development/CN=localhost"

# Instalar dependencias con PNPM
RUN pnpm install

# Exponer el puerto del servidor de desarrollo
EXPOSE 8088 

# Comando para iniciar el servidor
CMD ["pnpm", "run", "dev"]
