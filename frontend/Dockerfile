# Usa imagem oficial do Node 18
FROM node:18 as build

WORKDIR /app

# Copia e instala dependências
COPY package*.json ./
RUN npm install

# Copia código e faz build de produção (React)
COPY . .
RUN npm run build

# --- Servidor para servir build ---

FROM nginx:alpine

# Remove conteúdo padrão do nginx
RUN rm -rf /usr/share/nginx/html/*

# Copia build do React para nginx
COPY --from=build /app/build /usr/share/nginx/html

# Expõe porta 80
EXPOSE 80

# Inicia nginx
CMD ["nginx", "-g", "daemon off;"]
