# ??? API de Produtos Uma Penca ? Laravel 12

## ?? Sobre o Projeto

Esta é uma API REST desenvolvida em **Laravel 12**, com autenticação baseada em **Laravel Sanctum**.

### ? A API permite:

- ? Registro de usuário
- ? Login
- ? Logout
- ? CRUD completo de produtos
- ? Proteção de rotas autenticadas via token

## ??? Tecnologias Utilizadas

| Tecnologia | Versão |
|-----------|--------|
| PHP | 8+ |
| Laravel | 12.51.0 |
| MySQL | - |
| Laravel Sanctum | Autenticação via token |
| Postman | Para testes |

## ??? Decisões Técnicas

### 1?? Laravel Sanctum

Foi utilizado o Laravel Sanctum por ser a solução oficial do Laravel para autenticação via token em APIs REST.

### 2?? Estrutura RESTful

As rotas seguem o padrão REST:

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| POST | `/api/register` | Registrar usuário |
| POST | `/api/login` | Login |
| POST | `/api/logout` | Logout (protegido) |
| GET | `/api/products` | Listar produtos |
| GET | `/api/products/{id}` | Exibir produto |
| POST | `/api/products` | Criar produto |
| PUT | `/api/products/{id}` | Atualizar produto |
| DELETE | `/api/products/{id}` | Deletar produto |

### 3?? Proteção de Rotas

As rotas que modificam dados estão protegidas com:

```
auth:sanctum
```

Isso garante que apenas usuários autenticados possam criar, editar ou remover produtos.

## ?? Como Rodar o Projeto

### 1?? Clonar o repositório
```bash
git clone <url-do-repositorio>
cd nome-do-projeto
```

### 2?? Instalar dependências
```bash
composer install
```

### 3?? Configurar o `.env`
Copiar o arquivo de exemplo:
```bash
cp .env.example .env
```

### 4?? Configurar o banco de dados

No arquivo `.env`, adicione:
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=uma-penca
DB_USERNAME=seu_usuario
DB_PASSWORD=sua_senha
```

### 5?? Gerar chave da aplicação
```bash
php artisan key:generate
```

### 6?? Rodar as migrations
```bash
php artisan migrate
```

Isso criará as tabelas:
- `users`
- `personal_access_tokens`
- `products` (caso criada)

### 7?? Rodar o servidor
```bash
php artisan serve
```

A API estará disponível em:

```
http://127.0.0.1:8000
```

## ?? Fluxo de Autenticação

### ?? Registrar
**Endpoint:** `POST /api/register`

**Body (JSON):**
```json
{
  "name": "Usuario",
  "email": "usuario@email.com",
  "password": "123456"
}
```

### ?? Login
**Endpoint:** `POST /api/login`

**Retorna:**
```json
{
  "token": "token_gerado"
}
```

### ??? Usar Token nas Rotas Protegidas

Adicionar no Header:
```
Authorization: Bearer SEU_TOKEN_AQUI
```

### ?? Logout
**Endpoint:** `POST /api/logout`

Remove o token atual.


## ?? Estrutura Principal

```
app/
 ??? Http/Controllers/
 ?    ??? AuthController.php
 ?    ??? ProductController.php
routes/
 ??? api.php
database/
 ??? migrations/
```

## ? Considerações Finais

- ?? Código seguindo padrão MVC
- ?? Rotas separadas entre públicas e protegidas
- ?? Autenticação stateless via token
- ?? Estrutura preparada para fácil escalabilidade
- ?? API desenvolvida seguindo boas práticas REST