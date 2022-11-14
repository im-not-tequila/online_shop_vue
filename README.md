# online_shop_vue

В файле src/main.js в переменной axios.defaults.baseURL необходимо указать URL-адрес, на котором работает back-end

## Локальный запуск контейнера (http://localhost:8081)
```
docker-compose -f docker-compose-dev.yml up -d --build
```

### Production - запуск контейнера (http://внешний_ип_сервера:8081)
```
docker-compose -f docker-compose-prod.yml up -d --build
```

Back-end для данного приложения находится [тут](https://github.com/im-not-tequila/online_shop_django).
