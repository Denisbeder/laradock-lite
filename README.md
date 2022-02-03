# laradock-lite
Ambiente de desenvolvimento local laravel baseado em Docker

# Começo rápido
[instalar docker](https://docs.docker.com/docker-for-mac/install/)
Verifique se o docker-compose também está instalado corretamente
```
$docker-compose -v
versão do docker-compose 1.11.2, compilação dfed245
```
`composer global requer "laravel/installer"`

`laravel novo blog && cd $_`

Modifique a seção DB em .env
```
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=padrão
DB_USERNAME=padrão
DB_PASSWORD=segredo
```

`git clone https://github.com/denisbeder/laradock-lite.git && cd laradock-lite`

`cp env-example .env`

Modifique DOCKER_HOST_IP=172.16.30.1 no arquivo .env para seu ip local. Isso é usado principalmente para a função xdebug. A documentação da função xdebug pronta para uso será lançada posteriormente.

`docker-compose up` ou `docker-compose up -d`

Finalmente abra http://localhost no seu navegador

Execute o comando php artisan xxx:
```
espaço de trabalho do docker-compose exec /bin/ash
php artesão migrar: atualizar
```

# Componentes
Observando cada imagem em docker-compose.yml, você pode ver todos os componentes, onde cada componente é executado em seu próprio contêiner, ou seja, um componente por contêiner
1. nginx 1.12
2. php-fpm é baseado em php8.1
3. mysql 5.7
4. redis 3.2
5. pesquisa elástica 5.3.2 (nome de usuário e senha padrão do XPack elastic/changeme)

# Pontos não cobertos
Para projetos front-end, como React.js + webpack, é recomendado temporariamente usar npm ou yarn para instalar dependências de desenvolvimento localmente, consulte [create-react-app](https://github.com/facebookincubator/create-react-app) Início rápido.