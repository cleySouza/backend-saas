# ⚙️ beSyS — **Documentação do Backend**

## 🚀 1. Introdução

O backend do **beSyS** é desenvolvido com **Node.js + NestJS**, estruturado para oferecer alta segurança, modularidade, escalabilidade e facilidade de manutenção.

---

# 🧭 2. Diagramas Avançados

## 🏗️ 2.1 Diagrama Geral da Arquitetura Backend

```
                       ┌───────────────────────────┐
                       │         Frontends          │
                       │  Admin (PDV) / Cliente     │
                       └─────────────┬─────────────┘
                                     │ REST / JSON
                                     ▼
                        ┌────────────────────────┐
                        │      API Gateway       │
                        │ (NestJS Controllers)   │
                        └─────────────┬──────────┘
                                      │ calls
                                      ▼
                    ┌───────────────────────────────┐
                    │        Application Layer       │
                    │  (Services, Regras de Negócio) │
                    └─────────────┬──────────────────┘
                                    │ Prisma Client
                                    ▼
                      ┌─────────────────────────────┐
                      │         Data Layer           │
                      │        PostgreSQL/Prisma     │
                      └─────────────────────────────┘
```

---

## 🧩 2.2 Diagrama de Módulos

```
 backend/modules
 ├── auth
 │    ├── login
 │    ├── jwt
 │    └── rbac
 ├── users
 ├── companies
 ├── products
 ├── orders
 │    ├── pedido
 │    ├── status
 │    └── integração PDV
 ├── appointments
 └── cash-register
```

```
        ┌───────── auth ─────────┐
        │   JWT • Login • RBAC   │
        └──────────┬─────────────┘
                   ▼
   ┌──── users ────┬──── companies ────┐
   │               │                    │
   ▼               ▼                    ▼
 products → orders → appointments → cash-register
```

---

## 🔄 2.3 Fluxo de Autenticação (JWT)

```
[1] Cliente envia email/senha
        │
        ▼
[2] AuthService valida credenciais
        │
        ▼
[3] Geração de AccessToken + RefreshToken
        │
        ▼
[4] Resposta:
{
  accessToken,
  refreshToken,
  user
}
        │
        ▼
[5] Próximas requisições → Header: Authorization: Bearer TOKEN
```

---

## 📦 2.4 Fluxo de Pedido (Orders)

```
Cliente
  │
  ├─ POST /orders
  ▼
Backend
  │  Valida itens, preços, estoque
  │  Registra pedido
  ▼
Caixa / PDV
  │  Recebe notificação
  │  Atualiza status (pending → confirmed)
  ▼
Cliente recebe confirmação
```

---

## 📅 2.5 Fluxo de Agendamento (Appointments)

```
Cliente → Seleciona serviço
      → Envia data/hora desejada
                │
                ▼
         Backend verifica disponibilidade
                │
                ├── horário livre → cria agendamento
                └── horário ocupado → retorna erro
                ▼
       PDV recebe agendamento pendente
```

---

# 🧰 3. Tecnologias

* 🟩 **Node.js 18+**
* 🛡️ **NestJS**
* 🧩 **TypeScript**
* 🟦 **Prisma ORM**
* 🗄️ **PostgreSQL**
* 🔐 **JWT + RBAC**
* 🧪 **Class-validator** para DTOs
* 🧵 **Zod** (opcional)

---

# 🏗️ 4. Arquitetura Interna

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

---

# 🧩 5. Módulos do Sistema

### 🔐 Auth

### 👥 Users

### 🏢 Companies

### 🛒 Products

### 📦 Orders

### 📅 Appointments

### 💰 Cash Register

---

# 🗄️ 6. Banco de Dados (Prisma ORM)

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

# 🔗 7. APIs

```
/api/v1/auth/login
/api/v1/users
/api/v1/companies
/api/v1/products
/api/v1/orders
/api/v1/appointments
/api/v1/cash
```

---

# 🧪 8. Scripts

```
pnpm run start:dev
pnpm prisma migrate dev
pnpm prisma studio
```

---

# 🛡️ 9. Segurança

* bcrypt
* JWT + Refresh Token
* Guards + RBAC
* Rate limiting

---

# 🧭 10. Roadmap Backend

* [ ] RBAC avançado
* [ ] WebSockets
* [ ] Pagamentos
* [ ] E2E
* [ ] Multi-tenancy

---

Quer que eu adicione **diagramas UML**, **sequência detalhada**, ou **diagramas por módulo**?
