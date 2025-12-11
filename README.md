# 🛠️ Backend — Auth Service (NestJS)
## 🎯 Objetivo

Criar o serviço de autenticação e multi-tenancy, incluindo:

- Registro
- Login
- JWT Access Token
- Multi-Tenant via `tenantId`
- Models: User, Tenant
- Integração com PostgreSQL via Docker

🚀 Stack Técnica

NestJS

TypeORM + PostgreSQL

Docker + docker-compose

bcrypt

JWT (Passport + passport-jwt)

class-validator / class-transformer

📂 Estrutura do Auth Service
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

📘 Modelos
User

id

email

name

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

🔐 Fluxos Essenciais
Registro

Receber email, senha, nome e nome do tenant

Criar Tenant

Hash de senha (bcrypt)

Criar User como administrador do tenant

Retornar 201

Login

Validar email/senha

Checar tenant

Gerar JWT

Retornar token
