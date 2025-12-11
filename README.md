# beSyS — Documentação do Backend

## 1. Introdução

Backend do sistema beSyS, implementado em **Node.js + NestJS**, seguindo princípios de modularidade, segurança e escalabilidade. Este documento descreve a arquitetura interna, módulos, padrões e convenções.

---

## 2. Tecnologias

* **Node.js 18+**
* **NestJS**
* **TypeScript**
* **Prisma ORM**
* **PostgreSQL**
* **JWT / RBAC**
* **Zod (opcional)** para validação
* **Class-validator** para DTOs

---

## 3. Arquitetura Interna

Estrutura por módulos independentes (Domain-Driven Structure):

```
backend/
└─ src/
   ├─ app.module.ts
   ├─ main.ts
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

## 4. Módulos

### Auth

* Login por email/senha
* Tokens JWT
* Middleware + Guards de autorização

### Users

* Cadastro
* Perfil (admin, funcionário, cliente)
* Relacionamento com empresas

### Companies

* Configurações gerais
* Horários
* Temas

### Products / Services

* CRUD completo
* Categorias

### Orders

* Fluxo completo de pedido
* Status
* Integração com PDV

### Appointments

* Agendamento de serviços
* Verificação de disponibilidade

### Cash Register

* Abertura/fechamento
* Operações de caixa

---

## 5. Banco de Dados (Prisma)

Schema base:

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

## 6. APIs

Padrões:

```
/api/v1/auth/login
/api/v1/users
/api/v1/companies
/api/v1/products
/api/v1/orders
/api/v1/appointments
/api/v1/cash
```

Retornos padronizados:

```
{
  success: boolean,
  data?: any,
  message?: string,
  errors?: any
}
```

---

## 7. Scripts

```
pnpm run start:dev
pnpm prisma migrate dev
pnpm prisma studio
```

---

## 8. Segurança

* Hash com bcrypt
* JWT + Refresh Tokens (opcional)
* RBAC por decorator @Roles()
* Rate limiting por IP (middleware)

---

## 9. Roadmap Backend

* [ ] Finalizar RBAC avançado
* [ ] Adicionar WebSockets
* [ ] Adicionar integração com meios de pagamento
* [ ] Testes end-to-end (E2E)
