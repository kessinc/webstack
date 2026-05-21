# 🚀 Ultimate Next.js (App Router) Project Structure

Bu yapı; temiz kod prensipleri (Clean Code), özellik tabanlı ayrıştırma (Feature-based slicing) ve Next.js'in en gelişmiş yeteneklerini desteklemek üzere tasarlanmıştır.

```text
.
├── .github/                # CI/CD Workflows, Issue Templates
├── .husky/                  # Git Hooks (Pre-commit linting/testing)
├── public/                 # Statik dosyalar (Favicon, robots.txt, manifest.json)
│   ├── fonts/              # Local font dosyaları
│   ├── icons/              # SVG icon setleri
│   └── images/             # Optimize edilmemiş statik görseller
│
├── src/
│   ├── app/                # 📂 ROUTING LAYER (Next.js App Router)
│   │   ├── (auth)/         # Route Group: Kimlik doğrulama akışları
│   │   │   ├── login/
│   │   │   └── register/
│   │   ├── (dashboard)/    # Route Group: Uygulama içi yönetim paneli
│   │   │   ├── @analytics/ # Parallel Route: Aynı anda yüklenen dashboard slotu
│   │   │   ├── @notifications/
│   │   │   ├── layout.tsx
│   │   │   └── page.tsx
│   │   ├── (shop)/         # Route Group: E-ticaret / Ürün akışları
│   │   │   ├── products/
│   │   │   │   ├── [id]/   # Dynamic Route: Ürün detay
│   │   │   │   │   └── (...)photo/ # Intercepting Route: Modal ile ürün resmi açma
│   │   │   └── page.tsx
│   │   ├── api/            # API Route Handlers (Edge/Node.js Functions)
│   │   │   ├── auth/[...nextauth]/
│   │   │   └── webhooks/   # Stripe, Clerk vb. için webhooklar
│   │   ├── apple-icon.png  # Dinamik metadata dosyaları
│   │   ├── error.tsx       # Global Error Boundary
│   │   ├── global-error.tsx # Root layout hataları için özel dosya
│   │   ├── layout.tsx      # Root Layout (Providers burada sarmalanır)
│   │   ├── loading.tsx     # Global Streaming (Suspense)
│   │   ├── not-found.tsx   # 404 Sayfası
│   │   └── page.tsx        # Landing Page
│   │
│   ├── actions/            # ⚡ GLOBAL SERVER ACTIONS (Shared across features)
│   │   ├── email-actions.ts
│   │   └── upload-actions.ts
│   │
│   ├── components/         # 🧱 SHARED UI COMPONENTS
│   │   ├── ui/             # Shadcn/UI (Atomik, düşük seviyeli bileşenler)
│   │   ├── forms/          # Genel form yapıları (React Hook Form + Zod)
│   │   ├── layout/         # Navigation, Sidebar, Footer, UserMenu
│   │   ├── animations/     # Framer Motion sarmalayıcıları
│   │   ├── feedback/       # Toast, Dialog, Skeleton loaderlar
│   │   └── table/          # Data-table soyutlamaları (TanStack Table)
│   │
│   ├── features/           # 🧩 DOMAIN-DRIVEN MODULES (Business Logic)
│   │   ├── [feature-name]/
│   │   │   ├── actions.ts  # Feature-specific Server Actions
│   │   │   ├── api/        # Fetchers, React Query hooks
│   │   │   ├── components/ # Bu özelliğe has UI (örn: CartItem, OrderSummary)
│   │   │   ├── constants.ts
│   │   │   ├── hooks.ts    # useCart, useOrderManagement vb.
│   │   │   ├── schemas.ts  # Zod validation şemaları
│   │   │   ├── types.ts    # TypeScript interfaces
│   │   │   └── index.ts    # Public API (Sadece gerekli olanları dışarı aç)
│   │
│   ├── config/             # ⚙️ CONFIGURATION & ENV VALIDATION
│   │   ├── env.ts          # Zod ile Process.env doğrulaması (Type-safe env)
│   │   ├── site-config.ts  # SEO, Metadata, Sosyal linkler
│   │   └── constants.ts    # App-wide sabitler
│   │
│   ├── db/                 # 🗄️ DATABASE LAYER (ORM)
│   │   ├── schema/         # Drizzle/Prisma schema tanımları
│   │   ├── migrations/     # SQL göç dosyaları
│   │   ├── seed.ts         # Test verisi oluşturma
│   │   └── index.ts        # Database client (Singleton)
│   │
│   ├── hooks/              # ⚓ GLOBAL CUSTOM HOOKS
│   │   ├── use-media-query.ts
│   │   ├── use-mounted.ts
│   │   └── use-click-outside.ts
│   │
│   ├── lib/                # 📚 SDK & THIRD PARTY WRAPPERS
│   │   ├── stripe.ts       # Stripe client config
│   │   ├── resend.ts       # E-mail servis ayarları
│   │   ├── redis.ts        # Caching/Rate limiting
│   │   └── utils.ts        # Tailwind merge (cn), formatters vb.
│   │
│   ├── middleware.ts       # Auth guard, i18n redirect, logging
│   │
│   ├── providers/          # 🌐 CONTEXT PROVIDERS (Client-side)
│   │   ├── theme-provider.tsx # Next-themes (Dark mode)
│   │   ├── query-provider.tsx # TanStack Query
│   │   └── auth-provider.tsx  # NextAuth/Clerk Session
│   │
│   ├── services/           # 🛠️ EXTERNAL SERVICES (Abstraction layer)
│   │   ├── storage-service.ts # S3/Cloudinary soyutlaması
│   │   └── payment-service.ts
│   │
│   ├── styles/             # 🎨 STYLING
│   │   └── globals.css     # Tailwind katmanları (@layer)
│   │
│   ├── types/              # 🏷️ GLOBAL TYPES
│   │   └── common.ts       # API responses, Pagination types
│   │
│   └── utils/              # 🔧 PURE HELPER FUNCTIONS
│       ├── date.ts         # Dayjs/Date-fns helpers
│       └── number.ts       # Currency/Unit formatters
│
├── tests/                  # 🧪 TESTING SUITE
│   ├── unit/               # Vitest / Jest (Logic tests)
│   ├── integration/        # Component tests
│   └── e2e/                # Playwright / Cypress (User flows)
│
├── .env.example            # Çevre değişkenleri şablonu
├── next.config.mjs         # Next.js ana ayarları (Redirects, Image domains)
├── tailwind.config.ts      # Tasarım sistemi ayarları
└── tsconfig.json           # Path Aliases (@/* -> src/*)
```

---

## 💎 Profesyonel Mimari Prensipler

### 1. Server Actions vs. API Routes
*   **Actions:** Form gönderimleri ve kullanıcı etkileşimli veri değişiklikleri için `src/features/[feature]/actions.ts` kullanılır.
*   **API Routes:** Webhooklar, üçüncü parti entegrasyonlar veya mobil uygulamalar gibi dış sistemlerin erişeceği endpointler için `src/app/api` kullanılır.

### 2. Parallel ve Intercepting Routes
Modern dashboard tasarımlarında; bir sayfayı (örn: `/settings`) mevcut sayfanın üzerinde modal olarak açmak (`(.)settings`) veya sayfanın farklı bölümlerini farklı loading stateleri ile asenkron yüklemek (`@analytics`) için bu yapı kritiktir.

### 3. Type-Safe Environment Variables
`src/config/env.ts` içinde **Zod** kullanarak `.env` dosyandaki değişkenleri doğrula. Böylece eksik bir API anahtarı olduğunda uygulama build sırasında hata verir, runtime'da çökmez.

### 4. Module Boundaries (Giriş/Çıkış Kontrolü)
`features/` altındaki bir klasör, başka bir feature'ın içindeki bir dosyayı derinlemesine import etmemelidir. İhtiyaç duyulan her şey `features/[feature]/index.ts` üzerinden export edilmeli ve oradan tüketilmelidir.

### 5. Database & ORM Soyutlaması
Veritabanı mantığını `src/db` altında toplamak, yarın bir gün Prisma'dan Drizzle'a (veya tam tersi) geçerken uygulamanın geri kalanını korumanı sağlar.
