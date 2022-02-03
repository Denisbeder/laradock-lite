#laradock-lite
Ambiente de desenvolvimento local laravel baseado em Docker

# Prefácio
Meus requisitos para um ambiente de desenvolvimento local perfeito:

1. Inicie todos os componentes com um clique, sem necessidade de simular nenhum serviço, sem cliente fictício. Novas pessoas podem começar a desenvolver novos recursos dentro de uma hora após a integração.
2. Menos uso de recursos do sistema, ou seja, menos uso de CPU e memória, nenhum desenvolvimento travado no MacBook Pro
3. Isole o ambiente local e instale o mínimo de software dependente possível nesta máquina, por exemplo, não instale o mysql nesta máquina
4. Semelhante ao desenvolvimento integrado, teste de integração e ambientes de produção, é fácil solucionar problemas causados ​​pelo ambiente. As equipes usam uma configuração unificada de ambiente de desenvolvimento e teste para melhorar a eficiência da colaboração.
5. É fácil de depurar, seria melhor se pudesse ser integrado ao IDE
6. Funcionalidade REPL (língua limitada, é claro)
7. Teste de unidade fácil de executar
8. É fácil experimentar vários métodos de uso de serviço e servidor. Por exemplo, depois de iniciar rapidamente o servidor de pesquisa elástica, você pode aprender a usar es com base em um livro e um vídeo

# Origem
Ao desenvolver aplicações web com Laravel pela primeira vez, Homestead foi usado como ambiente de desenvolvimento local. Homestead é baseado em Vagrant e VirtualBox. Seja para configurar o ambiente de desenvolvimento sozinho ou para ajudar outros a configurá-lo, leva um certo tempo. Toda vez que uma nova pessoa entra, demora um pouco. Mais tarde, não testei o Valet recomendado na documentação oficial do laravel, visto que a documentação é baseada no Homebrew para instalar nesta máquina, eu pessoalmente não gosto de poluir o ambiente local, então ainda recorri à solução docker.

Quando descobri [laradock](https://github.com/laradock/laradock), fiquei impressionado e pensei que era exatamente o que eu estava procurando. Então experimente, muito feliz. Não vou repetir as vantagens do docker aqui, é a tendência geral usar o docker para construir ambientes de desenvolvimento, teste e produção. Atualmente, o docker é usado apenas no ambiente de desenvolvimento em meu projeto, e recursos adicionais de operação e manutenção são necessários para o ambiente de produção, e os mestres interessados ​​podem experimentá-lo.

Existem muitos componentes integrados no laradock.No processo de customização, apenas retiro os componentes que preciso e ao mesmo tempo reduzo o tamanho da imagem do docker com base na imagem alpina. Ao mesmo tempo, o xdebug é instalado para facilitar a depuração e o aprendizado do framework laravel.


# Quem é adequado
1. Novo no desenvolvimento laravel, aprenda laravel rapidamente
2. Desenvolvedores que pretendem usar isso como um ambiente de desenvolvimento local
3. Desenvolvedores que depuram o framework laravel e aprendem em profundidade

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

`git clone https://github.com/yangliuyu/laradock-lite.git && cd laradock-lite`

`cp env-example .env`

Modifique DOCKER_HOST_IP=172.16.30.1 no arquivo .env para seu ip local. Isso é usado principalmente para a função xdebug. A documentação da função xdebug pronta para uso será lançada posteriormente.

`docker-compose up` ou `docker-compose up -d`

Finalmente abra http://localhost no seu navegador

Execute o comando php artisan xxx:
```
espaço de trabalho do docker-compose exec /bin/ash
php artesão migrar: atualizar
```

# componentes
Observando cada imagem em docker-compose.yml, você pode ver todos os componentes, onde cada componente é executado em seu próprio contêiner, ou seja, um componente por contêiner
1. nginx 1.12
2. php-fpm é baseado em php7.1
3. mysql 5.7
4. redis 3.2
5. pesquisa elástica 5.3.2 (nome de usuário e senha padrão do XPack elastic/changeme)

# pontos não cobertos
Para projetos front-end, como React.js + webpack, é recomendado temporariamente usar npm ou yarn para instalar dependências de desenvolvimento localmente, consulte [create-react-app](https://github.com/facebookincubator/ create-react-app) Início rápido.

#escreve no final
O que combina com você é o melhor, e desejo a todos um momento feliz.