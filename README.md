# ⚙️ beSyS — **Documentação do Backend**

## 🚀 1. Introdução

O backend do **beSyS** é desenvolvido com **Node.js + NestJS**, estruturado para oferecer alta segurança, modularidade, escalabilidade e facilidade de manutenção.

Este documento detalha arquitetura interna, módulos, banco, padrões e roadmap.

---

## 🧰 2. Tecnologias Utilizadas

* 🟩 **Node.js 18+**
* 🛡️ **NestJS**
* 🧩 **TypeScript**
* 🟦 **Prisma ORM**
* 🗄️ **PostgreSQL**
* 🔐 **JWT + RBAC**
* 🧪 **Class-validator** para DTOs
* 🧵 **Zod** (opcional) para validações adicionais

---

## 🏗️ 3. Arquitetura Interna

A arquitetura segue o padrão **modular do NestJS**, inspirada em práticas de **DDD** (Domain-Driven Design).

```
backend/
└─ src/
   ├─ main.ts
   ├─ app.module.ts
   ├─ common/
   │  ├─ decorators/
   │  ├─ guards/
   │  ├─ interceptors/
   │  └─ filters/
   ├─ modules/
   │  ├─ auth/
   │  ├─ users/
   │  ├─ companies/
   │  ├─ products/
   │  ├─ orders/
   │  ├─ appointments/
   │  └─ cash-register/
   └─ prisma/
      ├─ prisma.module.ts
      └─ prisma.service.ts
```

Cada módulo possui:

* **controller** → rotas
* **service** → regras de negócio
* **dto** → validação
* **entities** (opcional)

---

## 🧩 4. Módulos do Sistema

### 🔐 Auth

* Login com email/senha
* Emissão de **JWT**
* Guards: `AuthGuard`, `RolesGuard`

### 👥 Users

* CRUD de usuários
* Perfis: `admin`, `employee`, `client`
* Relacionamento com Company

### 🏢 Companies

* Configurações gerais
* Horários e dados internos
* Temas personalizados

### 🛒 Products / Services

* CRUD completo
* Categorias
* Itens vendáveis e serviços agendáveis

### 📦 Orders

* Criação de pedidos
* Fluxo do PDV
* Status do pedido

### 📅 Appointments

* Agendamento de serviços
* Validação de disponibilidade
* Lista da agenda

### 💰 Cash Register

* Abertura/fechamento
* Operações de caixa
* Integração com pedidos

---

## 🗄️ 5. Banco de Dados (Prisma ORM)

Schema base simplificado:

```
model User {
  id          String   @id @default(cuid())
  name        String
  email       String   @unique
  password    String
  role        Role
  companyId   String?
  company     Company? @relation(fields: [companyId], references: [id])
}

model Company {
  id       String  @id @default(cuid())
  name     String
  users    User[]
}

enum Role {
  admin
  employee
  client
}
```

---

## 🔗 6. APIs

Rotas seguem padrão REST:

```
/api/v1/auth/login
/api/v1/users
/api/v1/companies
/api/v1/products
/api/v1/orders
/api/v1/appointments
/api/v1/cash
```

### 📤 Respostas padronizadas

```
{
  success: boolean,
  data?: any,
  message?: string,
  errors?: any
}
```

---

## 🧪 7. Scripts Úteis

```
pnpm run start:dev
pnpm prisma migrate dev
pnpm prisma studio
```

---

## 🛡️ 8. Segurança

* ✔️ Hash de senha com **bcrypt**
* 🔑 JWT Access Token + Refresh Token (opcional)
* 🧩 RBAC com decorator `@Roles()`
* 🚧 Rate limiting por IP
* 🛁 Sanitização via pipes

---

## 🧭 9. Roadmap Backend

* [ ] RBAC avançado com permissões granulares
* [ ] WebSockets para pedidos e agenda
* [ ] Integração com pagamentos
* [ ] Testes E2E com Jest + Supertest
* [ ] Multi-tenancy por schema

---

Se quiser, posso gerar **diagramas internos**, **exemplo real de módulo completo**, ou **estrutura do banco detalhada**! 🚀
