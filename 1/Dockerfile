# Используем базовый образ nginx версии 1.21.1
FROM nginx:1.21.1

# Удаляем стандартную страницу
RUN rm -rf /usr/share/nginx/html/*

# Копируем ваш index.html в директорию nginx
COPY index.html /usr/share/nginx/html/

# Указываем стандартный порт
EXPOSE 80
