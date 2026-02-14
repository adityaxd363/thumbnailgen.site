# Ecommerce Platform (Next.js + TypeScript + MongoDB)

## Step 1 — Project Folder Structure + Setup Commands

### 1) Create the project

```bash
# 1. Create Next.js app (App Router + TypeScript + Tailwind + ESLint)
npx create-next-app@latest ecommerce-app \
  --typescript \
  --tailwind \
  --eslint \
  --app \
  --src-dir \
  --use-npm \
  --import-alias "@/*"

# 2. Enter project directory
cd ecommerce-app

# 3. Install runtime dependencies
npm install mongoose zod bcryptjs jsonwebtoken cookie date-fns clsx

# 4. Install dev dependencies
npm install -D @types/jsonwebtoken @types/bcryptjs @types/node
```

### 2) Environment variables

Create `.env.local`:

```bash
MONGODB_URI=mongodb+srv://<user>:<pass>@cluster.mongodb.net/ecommerce
JWT_SECRET=replace_with_long_random_secret
ADMIN_EMAIL=admin@example.com
ADMIN_PASSWORD_HASH=<bcrypt_hash>

# Placeholder payment gateway keys (India gateway to be finalized in Step 5)
PAYMENT_KEY_ID=replace_me
PAYMENT_KEY_SECRET=replace_me
PAYMENT_WEBHOOK_SECRET=replace_me

NEXT_PUBLIC_APP_URL=http://localhost:3000
```

### 3) Recommended production-oriented folder structure

```text
ecommerce-app/
├── public/
│   ├── products/
│   └── uploads/
├── src/
│   ├── app/
│   │   ├── (store)/
│   │   │   ├── page.tsx
│   │   │   ├── product/[slug]/page.tsx
│   │   │   ├── cart/page.tsx
│   │   │   ├── checkout/page.tsx
│   │   │   └── order-success/page.tsx
│   │   ├── admin/
│   │   │   ├── login/page.tsx
│   │   │   ├── dashboard/page.tsx
│   │   │   ├── products/page.tsx
│   │   │   ├── products/new/page.tsx
│   │   │   ├── products/[id]/edit/page.tsx
│   │   │   ├── orders/page.tsx
│   │   │   └── orders/[id]/page.tsx
│   │   ├── api/
│   │   │   ├── auth/login/route.ts
│   │   │   ├── products/route.ts
│   │   │   ├── products/[id]/route.ts
│   │   │   ├── cart/route.ts
│   │   │   ├── checkout/create-order/route.ts
│   │   │   ├── payments/create-order/route.ts
│   │   │   ├── payments/webhook/route.ts
│   │   │   ├── orders/route.ts
│   │   │   ├── orders/[id]/route.ts
│   │   │   └── admin/dashboard/route.ts
│   │   ├── globals.css
│   │   └── layout.tsx
│   ├── components/
│   │   ├── ui/
│   │   ├── store/
│   │   └── admin/
│   ├── lib/
│   │   ├── db.ts
│   │   ├── auth.ts
│   │   ├── api-response.ts
│   │   ├── payment/
│   │   └── validators/
│   ├── models/
│   │   ├── Product.ts
│   │   ├── Order.ts
│   │   └── Payment.ts
│   ├── middleware.ts
│   ├── types/
│   └── hooks/
├── .env.local
├── package.json
├── next.config.ts
├── tailwind.config.ts
└── tsconfig.json
```

### 4) Baseline scripts

Ensure these scripts exist in `package.json`:

```json
{
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  }
}
```

### 5) Run locally

```bash
npm install
npm run dev
```

Then open `http://localhost:3000`.


### 6) Preview kaise dekhein? (Hindi)

Agar aap local preview dekhna chahte ho, yeh exact steps follow karo:

```bash
# project folder ke andar
npm install
npm run dev
```

Ab browser me kholo:
- `http://localhost:3000`

Agar `localhost` open na ho, to yeh try karo:
- `http://127.0.0.1:3000`

Agar mobile ya same Wi-Fi ke dusre device par preview dekhna ho:

```bash
npm run dev -- -H 0.0.0.0 -p 3000
```

Phir apne system ka local IP open karo (example):
- `http://192.168.1.20:3000`

### 7) Common preview issues

- Port busy error aaye to:
  ```bash
  npm run dev -- -p 3001
  ```
  Aur phir `http://localhost:3001` open karo.

- Dependencies missing error aaye to:
  ```bash
  rm -rf node_modules package-lock.json
  npm install
  npm run dev
  ```


---

This completes **Step 1 only**. Next step will implement the Mongoose models (`Product`, `Order`, `Payment`) and shared database utilities.
