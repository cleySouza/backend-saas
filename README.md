# 🛠️ Backend — Auth Service (NestJS)
### 🎯 Objetivo

Criar o **serviço de autenticação e multi-tenancy**, incluindo:

- Registro
- Login
- JWT Access Token
- Multi-Tenant via `tenantId`
- Models: User, Tenant
- Integração com PostgreSQL via Docker

## 🚀 Stack Técnica

- **NestJS**
- **TypeORM** + PostgreSQL
- **Docker + docker-compose**
- **bcrypt**
- **JWT (Passport + passport-jwt)**
- **class-validator / class-transformer**

## 📂 Estrutura do Auth Service
```
services/auth-service/
├── src/
│   ├── auth/
│   │   ├── auth.controller.ts
│   │   ├── auth.service.ts
│   │   ├── auth.module.ts
│   │   └── strategies/
│   ├── user/
│   ├── tenant/
│   ├── database/
│   └── main.ts
├── Dockerfile
└── docker-compose.yml
```

### 📘 Modelos
#### User
- id
- email
- name
- passwordHash
- role
- tenantId
- createdAt
- updatedAt

#### Tenant
- id
- name
- slug
- plan
- createdAt

## 🔐 Fluxos Essenciais

### Registro
1. Receber email, senha, nome e nome do tenant
2. Criar Tenant
3. Hash de senha (bcrypt)
4. Criar User como administrador do tenant
5. Retornar 201

### Login
1. Validar email/senha
2. Checar tenant
3. Gerar JWT
4. Retornar token
