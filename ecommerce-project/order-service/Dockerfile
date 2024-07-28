# Usa a imagem base do Nginx
FROM nginx:alpine

# Remove a configuração padrão do Nginx
RUN rm /etc/nginx/conf.d/default.conf

# Copia a configuração personalizada do Nginx
COPY ../confi.d/default.config /etc/nginx/conf.d/default.conf

# Copia os arquivos estáticos para a pasta correta
COPY dist /usr/share/nginx/html

# Exponhe a porta 80
EXPOSE 80

# Inicia o Nginx
CMD ["nginx", "-g", "daemon off;"]
