# 🛠️ Documentação — Backend (Auth Service)
## 🎯 Objetivo do Backend Inicial

#### Construir o Auth Service completo com:

Registro

Login

Multi-Tenancy

JWT Access Token

Refresh Token (opcional depois)

User model

Tenant model

#### 🚀 Stack Técnica
NestJS

Framework backend robusto — estrutura modular, testes nativos, DI completo.

TypeORM + PostgreSQL

PostgreSQL como DB primário

TypeORM para migrations e models

Docker + docker-compose

Container para:

Auth Service

PostgreSQL

(Futuro) Redis para blacklist de tokens

Validations

class-validator

class-transformer

Auth

@nestjs/passport

passport-jwt

bcrypt

#### 🗂️ Estrutura do Auth Service
```services/auth-service/
├── src/
│   ├── auth/
│   │   ├── auth.controller.ts
│   │   ├── auth.service.ts
│   │   ├── auth.module.ts
│   │   └── strategies/
│   ├── user/
│   ├── tenant/
│   ├── prisma/ or typeorm/
│   └── main.ts
├── Dockerfile
└── docker-compose.yml
```
#### 📘 Modelos principais
User

id

name

email

passwordHash

role

tenantId

createdAt

updatedAt

Tenant

id

name

slug

plan

createdAt

### 🔐 Fluxos Essenciais do Backend
Registro

Receber email/senha/nome

Validar tenant

Hash da senha (bcrypt)

Criar User + Tenant

Retornar 201

Login

Validar email/senha

Validar tenant

Emitir JWT (payload: userId + tenantId)

Retornar tokens
