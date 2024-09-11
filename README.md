# Laravel Sail with Breeze, React, PHPUnit, and MySQL

Este projeto é uma aplicação Laravel que utiliza Laravel Sail para gerenciamento de containers Docker, Laravel Breeze para autenticação, React para o frontend, PHPUnit para testes e MySQL como banco de dados.

## Requisitos

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- [Node.js](https://nodejs.org/) (para o React)
- [Composer](https://getcomposer.org/) (para o Laravel)

## Instalação

### 1. Clonar o repositório

Clone o repositório para sua máquina local:

```bash
git clone https://github.com/SeuUsuario/sail-react-laravel.git
cd sail-react-laravel

```

### 2. Configurar o ambiente

```bash
cp .env.example .env

```

### 3. Configurar as variáveis de ambiente

Abra o arquivo .env e ajuste as configurações do banco de dados e outras variáveis de ambiente conforme necessário. Certifique-se de que a configuração do banco de dados está correta para o MySQL.

### 4. Construir e iniciar os containers

Utilize Laravel Sail para construir e iniciar os containers Docker:

```bash
./vendor/bin/sail up -d
```

Ou caso você tenha um alias para o sail, utilise seu alias.

### 5. Instalar as dependências do PHP

```bash
./vendor/bin/sail composer install
```
### 6. Instalar as dependências do Node.js

```bash
./vendor/bin/sail npm install
```

### 7. Rodar as migrações do banco de dados

Execute as migrações para criar as tabelas no banco de dados:

```bash
./vendor/bin/sail php artisan migrate
```

### 8. Ajuste a configuração do vite.config.js para funcionar com o sail:

No projeto, está configurado para funcionar com localhost.

```javascript
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';
import react from '@vitejs/plugin-react';

export default defineConfig({
    plugins: [
        laravel({
            input: 'resources/js/app.tsx',
            ssr: 'resources/js/ssr.tsx',
            refresh: true,
        }),
        react(),
    ],
    watch: {
        usePolling: true,
        origin: 'http://localhost'
    },
    server: {
        hmr: {
            host: 'localhost'
        }
    }
});
```

### 9. Compilar os assets do React

```bash
./vendor/bin/sail npm run dev
```