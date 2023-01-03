<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

<p align="center">
<a href="https://travis-ci.org/laravel/framework"><img src="https://travis-ci.org/laravel/framework.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>

## Sobre o Framework Laravel

Laravel é um framework de aplicações web com sintaxe expressiva e elegante. Acreditamos que o desenvolvimento deve ser uma experiência agradável e criativa para ser verdadeiramente gratificante. O Laravel simplifica o desenvolvimento facilitando tarefas comuns usadas em muitos projetos da web, como:

- [Motor de roteamento simples e rápido.](https://laravel.com/docs/routing).
- [Contêiner poderoso de injeção de dependência.](https://laravel.com/docs/container).
- Múltiplos back-ends para sessão e armazenamento em cache. (https://laravel.com/docs/session) and [cache](https://laravel.com/docs/cache) storage.
- ORM de banco de dados expressivo e intuitivo.(https://laravel.com/docs/eloquent).
- Migrações de esquema agnóstico de banco de dados.(https://laravel.com/docs/migrations).
- [Processamento robusto de trabalhos em segundo plano.](https://laravel.com/docs/queues).
- [Transmissão de eventos em tempo real.](https://laravel.com/docs/broadcasting).

<p> Abrir projeto no Gitpod: </p>

[![Gitpod Ready-to-Code](https://img.shields.io/badge/Gitpod-Ready--to--Code-blue?logo=gitpod)](https://gitpod.io/#https://github.com/paulocaetanomt88/testando-gitpod)


## Como integrar um projeto Laravel para codificação e testes no Gitpod

### Apresentação
Gitpod é uma plataforma SaaS que oferece ambientes de desenvolvimento Ready-To-Code. O que isso significa é que o GitPod permite que você descreva seu ambiente de desenvolvimento como código e o provisione ou compartilhe facilmente.

Isso é ótimo para permitir que as pessoas experimentem rapidamente uma nova biblioteca ou estrutura e até mesmo para o desenvolvimento do dia a dia.

Este artigo do blog do GitPod é uma ótima explicação para o problema que o GitPod resolve, bem como um fantástico guia de uso geral.

Aqui, vamos estender isso especificamente para o framework Laravel e ver como criar um ambiente Ready-To-Code para nossos projetos.

### Começando
A primeira etapa é navegar até o repositório do GitHub que você deseja configurar.

Para este exemplo, usarei este mesmo repositório mas você pode usar este ou outro de sua preferência.

O repositório GitHub está disponível publicamente em https://github.com/paulocaetanomt88/testando-gitpod/.

Em seguida, editaremos ligeiramente esta URL para iniciar um espaço de trabalho do Gitpod para este repositório.

Adicionaremos "gitpod.io/#" na frente da URL do repositório e pressionaremos enter. Para o exemplo acima, será https://gitpod.io/#https://github.com/paulocaetanomt88/testando-gitpod

Para usuários iniciantes do Gitpod, você será solicitado a entrar no GitHub e autorizar o aplicativo.

Quando vamos para este URL, o Gitpod começa a construir nosso espaço de trabalho e você verá a tela inicial.

Para determinar como configurar o ambiente, o Gitpod segue as instruções em um arquivo .gitpod.yml. Se esse arquivo não existir, ele se aproxima de um ambiente com base em seu repositório.

### Criar o .gitpod.Dockerfile
```
FROM gitpod/workspace-mysql               

USER gitpod
```
Isso usa o gitpod/workspace-mysql como a imagem base. Esta imagem instala e configura o MySQL com um usuário root sem senha.
Funciona para obter um ambiente com (quase) tudo o que você precisa, mas ainda há algumas tarefas básicas de manutenção que a maioria dos aplicativos Laravel precisará cuidar.

### Configurar .gitpod-init.sh e .gitpod.yml
Estes arquivos especificam os comandos que o ambiente deve executar na compilação, bem como o Dockerfile a ser usado para criar o contêiner. Adicionar um Dockerfile personalizado é opcional, mas potencialmente nos oferece mais controle sobre o ambiente com o qual terminamos.

Portanto, criaremos dois arquivos: um .gitpod-init.sh (que contém a sequência de linhas de comando) e um .gitpod.yml simples com o seguinte:

### Arquivo .gitpod-init.sh
```
mysql -u root -e "create database testando gitpod com laravel"
cp .env.example .env
sed -i "s|APP_URL=|APP_URL=${GITPOD_WORKSPACE_URL}|g" .env
sed -i "s|APP_URL=https://|APP_URL=https://8000-|g" .env
php artisan key:generate
composer install
npm install
```

### Arquivo .gitpod.yml
```
image:
  file: .gitpod.Dockerfile
tasks:
  - init: bash .gitpod-init.sh
    command: php artisan migrate --seed && php artisan serve
```

<p> Abrir projeto no Gitpod: </p>

[![Gitpod Ready-to-Code](https://img.shields.io/badge/Gitpod-Ready--to--Code-blue?logo=gitpod)](https://gitpod.io/#https://github.com/paulocaetanomt88/testando-gitpod)
