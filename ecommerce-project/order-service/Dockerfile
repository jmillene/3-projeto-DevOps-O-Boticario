# Utiliza a imagem base do Nginx
FROM nginx:alpine

# Define o diretório de trabalho dentro do container
WORKDIR /usr/share/nginx/html

# Copia os arquivos estáticos para o diretório de trabalho
COPY ./dist .

# Expõe a porta 80 para acesso ao serviço
EXPOSE 80
