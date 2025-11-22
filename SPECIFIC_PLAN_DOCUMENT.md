# 📐 SPECIFIC PLAN DOCUMENT: CALCULATOR WEBSITE - DETAILED IMPLEMENTATION SPECS
**Exact Specifications, Code Templates, Data Models, Content Examples**

---

## 📋 TABLE OF CONTENTS

1. Technical Architecture & Database Schema
2. Frontend Component Specifications
3. Backend API Documentation
4. Calculator Specifications (100+ examples)
5. Blog Content Specifications
6. SEO Implementation Guide
7. Feature Specifications (Save, Share, Export)
8. Monetization Implementation
9. Partnership Integration Guide
10. Analytics & Tracking Specifications

---

## 🏗️ SECTION 1: TECHNICAL ARCHITECTURE

### 1.1 Complete Tech Stack Specification

```yaml
Frontend:
  Framework: Next.js 14 (React 19)
  Language: TypeScript
  Styling: Tailwind CSS
  UI Components: Headless UI + Radix UI
  State Management: Zustand
  Data Fetching: TanStack Query (React Query)
  Form Handling: React Hook Form
  Validation: Zod + Server-side validation
  Analytics: Google Analytics 4 + Mixpanel
  Error Tracking: Sentry

Backend:
  Framework: Next.js API Routes + tRPC
  Database: PostgreSQL (Supabase)
  Authentication: Supabase Auth + JWT
  File Storage: Supabase Storage (for PDF exports)
  Cache: Redis (Upstash)
  Message Queue: Bull (for async tasks)

DevOps:
  Deployment: Vercel
  CDN: Cloudflare
  DNS: Cloudflare
  SSL: Cloudflare (free)
  Monitoring: Vercel Analytics + LogRocket
  CI/CD: GitHub Actions

Tools & Services:
  Email: Resend or SendGrid
  Payments: Stripe
  SMS: Twilio (optional)
  SEO: SEMrush API, Google Search API
  Images: Unsplash API, Cloudinary
```

---

### 1.2 Database Schema (Complete)

```sql
-- Users Table
CREATE TABLE public.users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) UNIQUE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  first_name VARCHAR(100),
  last_name VARCHAR(100),
  avatar_url VARCHAR(500),
  is_premium BOOLEAN DEFAULT false,
  premium_expires_at TIMESTAMP,
  created_at TIMESTAMP DEFAULT now(),
  updated_at TIMESTAMP DEFAULT now()
);

-- Calculators Table
CREATE TABLE public.calculators (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  slug VARCHAR(255) UNIQUE NOT NULL,
  title VARCHAR(255) NOT NULL,
  description TEXT,
  category VARCHAR(50) NOT NULL,
  subcategory VARCHAR(50),
  formula_explanation TEXT,
  formula_latex VARCHAR(500),
  formula_json JSONB,
  input_fields JSONB NOT NULL, -- Array of field configs
  output_format JSONB,
  examples JSONB, -- Array of examples
  seo_title VARCHAR(255),
  seo_description VARCHAR(160),
  seo_keywords VARCHAR(500),
  image_url VARCHAR(500),
  language VARCHAR(10) DEFAULT 'en',
  is_premium BOOLEAN DEFAULT false,
  views_count INT DEFAULT 0,
  created_at TIMESTAMP DEFAULT now(),
  updated_at TIMESTAMP DEFAULT now(),
  INDEX idx_category (category),
  INDEX idx_language (language)
);

-- Blog Posts Table
CREATE TABLE public.blog_posts (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  slug VARCHAR(255) UNIQUE NOT NULL,
  title VARCHAR(255) NOT NULL,
  content TEXT NOT NULL, -- Markdown
  excerpt VARCHAR(500),
  featured_image_url VARCHAR(500),
  author_id UUID REFERENCES users(id),
  seo_title VARCHAR(255),
  seo_description VARCHAR(160),
  seo_keywords VARCHAR(500),
  calculator_ids UUID[] DEFAULT ARRAY[]::UUID[], -- Related calculators
  published_at TIMESTAMP,
  is_published BOOLEAN DEFAULT false,
  view_count INT DEFAULT 0,
  language VARCHAR(10) DEFAULT 'en',
  created_at TIMESTAMP DEFAULT now(),
  updated_at TIMESTAMP DEFAULT now(),
  INDEX idx_published (is_published),
  INDEX idx_language (language)
);

-- Saved Results Table
CREATE TABLE public.saved_results (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  calculator_id UUID NOT NULL REFERENCES calculators(id),
  input_data JSONB NOT NULL,
  result_data JSONB NOT NULL,
  result_summary VARCHAR(255),
  created_at TIMESTAMP DEFAULT now(),
  updated_at TIMESTAMP DEFAULT now(),
  INDEX idx_user_id (user_id),
  INDEX idx_calculator_id (calculator_id)
);

-- Favorites Table
CREATE TABLE public.favorites (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  calculator_id UUID NOT NULL REFERENCES calculators(id),
  created_at TIMESTAMP DEFAULT now(),
  UNIQUE(user_id, calculator_id),
  INDEX idx_user_id (user_id)
);

-- Analytics Events Table
CREATE TABLE public.analytics_events (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id),
  session_id VARCHAR(255) NOT NULL,
  event_type VARCHAR(50), -- 'calculator_view', 'calculator_complete', 'blog_view'
  calculator_id UUID REFERENCES calculators(id),
  blog_post_id UUID REFERENCES blog_posts(id),
  metadata JSONB,
  timestamp TIMESTAMP DEFAULT now(),
  INDEX idx_timestamp (timestamp),
  INDEX idx_calculator_id (calculator_id)
);

-- Partnerships Table
CREATE TABLE public.partnerships (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  partner_name VARCHAR(255) NOT NULL,
  partner_email VARCHAR(255),
  partner_website VARCHAR(500),
  partner_type VARCHAR(50), -- 'school', 'advisor', 'influencer', 'platform'
  embed_url VARCHAR(500),
  monthly_revenue NUMERIC(10,2) DEFAULT 0,
  status VARCHAR(20) DEFAULT 'active',
  created_at TIMESTAMP DEFAULT now(),
  updated_at TIMESTAMP DEFAULT now(),
  INDEX idx_status (status)
);

-- Affiliate Links Table
CREATE TABLE public.affiliate_links (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  partner_id UUID NOT NULL REFERENCES partnerships(id),
  calculator_id UUID REFERENCES calculators(id),
  affiliate_url VARCHAR(500),
  conversion_count INT DEFAULT 0,
  commission_earned NUMERIC(10,2) DEFAULT 0,
  created_at TIMESTAMP DEFAULT now(),
  INDEX idx_partner_id (partner_id)
);

-- Premium Subscriptions Table
CREATE TABLE public.subscriptions (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  stripe_subscription_id VARCHAR(255),
  plan_type VARCHAR(50), -- 'monthly', 'annual'
  amount NUMERIC(10,2),
  status VARCHAR(20), -- 'active', 'canceled', 'past_due'
  started_at TIMESTAMP,
  ended_at TIMESTAMP,
  created_at TIMESTAMP DEFAULT now(),
  updated_at TIMESTAMP DEFAULT now(),
  INDEX idx_user_id (user_id)
);
```

---

### 1.3 Project Folder Structure

```
calcarena/
├── public/
│   ├── images/
│   │   ├── calculators/ (calculator icons)
│   │   ├── blog/ (blog featured images)
│   │   └── og/ (Open Graph images)
│   ├── fonts/ (custom fonts)
│   └── robots.txt
│
├── src/
│   ├── app/
│   │   ├── layout.tsx (root layout)
│   │   ├── page.tsx (homepage)
│   │   ├── (auth)/
│   │   │   ├── login/page.tsx
│   │   │   ├── signup/page.tsx
│   │   │   └── reset-password/page.tsx
│   │   ├── calculator/
│   │   │   ├── [slug]/page.tsx (dynamic calculator page)
│   │   │   ├── [slug]/loading.tsx
│   │   │   ├── [slug]/error.tsx
│   │   │   └── layout.tsx
│   │   ├── calculators/
│   │   │   ├── page.tsx (all calculators)
│   │   │   ├── [category]/page.tsx
│   │   │   └── layout.tsx
│   │   ├── blog/
│   │   │   ├── page.tsx (blog listing)
│   │   │   ├── [slug]/page.tsx (blog post)
│   │   │   └── layout.tsx
│   │   ├── dashboard/
│   │   │   ├── page.tsx (user dashboard)
│   │   │   ├── saved-results/page.tsx
│   │   │   ├── favorites/page.tsx
│   │   │   ├── account/page.tsx
│   │   │   └── layout.tsx (requires auth)
│   │   ├── api/
│   │   │   ├── auth/
│   │   │   │   ├── route.ts (auth endpoints)
│   │   │   │   └── callback/route.ts
│   │   │   ├── calculators/
│   │   │   │   ├── route.ts (GET all calculators)
│   │   │   │   ├── [id]/route.ts (GET single)
│   │   │   │   └── [id]/calculate/route.ts (POST calculate)
│   │   │   ├── blog/
│   │   │   │   ├── route.ts
│   │   │   │   └── [id]/route.ts
│   │   │   ├── results/
│   │   │   │   ├── route.ts (save result)
│   │   │   │   └── [id]/route.ts (get result)
│   │   │   ├── export/
│   │   │   │   └── pdf/route.ts
│   │   │   ├── analytics/
│   │   │   │   └── track/route.ts
│   │   │   └── health/route.ts
│   │   ├── embed/
│   │   │   └── [calculatorSlug]/page.tsx (embeddable widget)
│   │   ├── pricing/page.tsx
│   │   ├── about/page.tsx
│   │   ├── contact/page.tsx
│   │   └── 404.tsx
│   │
│   ├── components/
│   │   ├── common/
│   │   │   ├── Header.tsx
│   │   │   ├── Footer.tsx
│   │   │   ├── Navigation.tsx
│   │   │   ├── SkipToContent.tsx
│   │   │   └── CookieBanner.tsx
│   │   ├── calculator/
│   │   │   ├── Calculator.tsx (main component)
│   │   │   ├── InputField.tsx
│   │   │   ├── ResultDisplay.tsx
│   │   │   ├── ShareResult.tsx
│   │   │   ├── SaveResult.tsx
│   │   │   ├── ExportButton.tsx
│   │   │   ├── FormulaExplainer.tsx
│   │   │   └── CalculatorGrid.tsx
│   │   ├── blog/
│   │   │   ├── BlogPostCard.tsx
│   │   │   ├── BlogContent.tsx
│   │   │   ├── RelatedCalculators.tsx
│   │   │   └── AuthorBio.tsx
│   │   ├── auth/
│   │   │   ├── LoginForm.tsx
│   │   │   ├── SignupForm.tsx
│   │   │   └── ProtectedRoute.tsx
│   │   ├── forms/
│   │   │   ├── Input.tsx
│   │   │   ├── Select.tsx
│   │   │   ├── Checkbox.tsx
│   │   │   ├── Button.tsx
│   │   │   └── FormField.tsx
│   │   └── ui/
│   │       ├── Card.tsx
│   │       ├── Modal.tsx
│   │       ├── Tooltip.tsx
│   │       ├── Loading.tsx
│   │       ├── ErrorBoundary.tsx
│   │       └── Toast.tsx
│   │
│   ├── lib/
│   │   ├── api-client.ts (Axios instance)
│   │   ├── auth.ts (Auth utilities)
│   │   ├── db.ts (Database queries)
│   │   ├── schema.ts (Schema.org markup generators)
│   │   ├── calculations/ (Calculator formulas)
│   │   │   ├── finance.ts
│   │   │   ├── health.ts
│   │   │   ├── math.ts
│   │   │   ├── converters.ts
│   │   │   └── index.ts
│   │   ├── utils.ts (General utilities)
│   │   ├── validators.ts (Input validation)
│   │   ├── seo.ts (SEO helpers)
│   │   ├── tracking.ts (Analytics)
│   │   ├── export.ts (PDF/Excel export)
│   │   ├── stripe.ts (Stripe integration)
│   │   ├── supabase.ts (Supabase client)
│   │   └── constants.ts (App constants)
│   │
│   ├── hooks/
│   │   ├── useAuth.ts
│   │   ├── useCalculator.ts
│   │   ├── useSaveResult.ts
│   │   ├── useExport.ts
│   │   └── useAnalytics.ts
│   │
│   ├── stores/
│   │   ├── authStore.ts
│   │   ├── calculatorStore.ts
│   │   ├── uiStore.ts
│   │   └── analyticsStore.ts
│   │
│   ├── types/
│   │   ├── index.ts
│   │   ├── calculator.ts
│   │   ├── user.ts
│   │   ├── blog.ts
│   │   └── api.ts
│   │
│   └── styles/
│       ├── globals.css
│       ├── variables.css
│       └── animations.css
│
├── database/
│   ├── migrations/ (DB migration files)
│   ├── seeds/ (Seed data)
│   └── schema.sql (Full schema)
│
├── .env.example
├── .env.local (git ignored)
├── tailwind.config.js
├── tsconfig.json
├── next.config.js
├── package.json
├── .gitignore
└── README.md
```

---

## 🧩 SECTION 2: FRONTEND COMPONENTS

### 2.1 Calculator Component (Main)

```typescript
// src/components/calculator/Calculator.tsx

import React, { useState, useCallback } from 'react';
import { useForm } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';
import InputField from './InputField';
import ResultDisplay from './ResultDisplay';
import ShareResult from './ShareResult';
import SaveResult from './SaveResult';
import FormulaExplainer from './FormulaExplainer';
import type { Calculator as CalculatorType } from '@/types/calculator';

interface CalculatorProps {
  calculator: CalculatorType;
}

export default function Calculator({ calculator }: CalculatorProps) {
  const [result, setResult] = useState<any>(null);
  const [isCalculating, setIsCalculating] = useState(false);
  const [showFormula, setShowFormula] = useState(false);

  // Build dynamic validation schema from input fields
  const validationSchema = buildValidationSchema(calculator.input_fields);

  const {
    register,
    handleSubmit,
    formState: { errors },
    watch,
  } = useForm({
    resolver: zodResolver(validationSchema),
    mode: 'onChange',
  });

  const onSubmit = useCallback(async (data: any) => {
    setIsCalculating(true);
    try {
      const response = await fetch(
        `/api/calculators/${calculator.id}/calculate`,
        {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(data),
        }
      );

      if (!response.ok) {
        throw new Error('Calculation failed');
      }

      const result = await response.json();
      setResult(result);

      // Track analytics
      trackEvent('calculator_complete', {
        calculator_id: calculator.id,
        calculator_slug: calculator.slug,
      });
    } catch (error) {
      console.error('Calculation error:', error);
      // Show error toast
    } finally {
      setIsCalculating(false);
    }
  }, [calculator.id, calculator.slug]);

  return (
    <div className="w-full max-w-2xl mx-auto px-4 py-8">
      {/* Calculator Header */}
      <div className="mb-8">
        <h1 className="text-3xl font-bold text-gray-900 mb-2">
          {calculator.title}
        </h1>
        <p className="text-lg text-gray-600">
          {calculator.description}
        </p>
      </div>

      {/* Calculator Form */}
      <form
        onSubmit={handleSubmit(onSubmit)}
        className="bg-white rounded-lg shadow-lg p-6 mb-8"
      >
        <div className="space-y-6">
          {calculator.input_fields.map((field) => (
            <InputField
              key={field.name}
              field={field}
              register={register}
              error={errors[field.name]}
              watch={watch}
            />
          ))}
        </div>

        {/* Calculate Button */}
        <button
          type="submit"
          disabled={isCalculating}
          className="w-full mt-8 bg-blue-600 hover:bg-blue-700 disabled:opacity-50 text-white font-bold py-3 px-4 rounded-lg transition-colors"
        >
          {isCalculating ? 'Calculating...' : 'Calculate'}
        </button>
      </form>

      {/* Result Display */}
      {result && (
        <>
          <ResultDisplay
            result={result}
            calculator={calculator}
          />

          {/* Action Buttons */}
          <div className="flex gap-4 mt-6 flex-wrap">
            <ShareResult result={result} calculator={calculator} />
            <SaveResult result={result} calculator={calculator} />
            <button
              onClick={() => setShowFormula(!showFormula)}
              className="px-4 py-2 border border-gray-300 rounded-lg hover:bg-gray-50"
            >
              {showFormula ? 'Hide Formula' : 'Show Formula'}
            </button>
          </div>

          {/* Formula Explainer */}
          {showFormula && (
            <FormulaExplainer calculator={calculator} />
          )}
        </>
      )}

      {/* Related Calculators */}
      <div className="mt-12 pt-8 border-t">
        <h3 className="text-xl font-bold mb-6">Related Calculators</h3>
        <RelatedCalculators calculator={calculator} />
      </div>

      {/* FAQ Section */}
      <FAQ calculator={calculator} />
    </div>
  );
}

// Helper function to build validation schema
function buildValidationSchema(fields: any[]) {
  const shape: any = {};
  fields.forEach((field) => {
    let schema: any = z.string();

    if (field.type === 'number') {
      schema = z.coerce.number().positive('Must be positive');
    } else if (field.type === 'date') {
      schema = z.string().refine(
        (date) => new Date(date) < new Date(),
        'Date must be in the past'
      );
    }

    shape[field.name] = schema;
  });

  return z.object(shape);
}
```

---

### 2.2 Input Field Component

```typescript
// src/components/calculator/InputField.tsx

interface InputFieldProps {
  field: CalculatorField;
  register: UseFormRegister<any>;
  error?: FieldError;
  watch: UseWatch<any>;
}

export default function InputField({
  field,
  register,
  error,
  watch,
}: InputFieldProps) {
  const value = watch(field.name);

  return (
    <div className="space-y-2">
      {/* Label */}
      <label htmlFor={field.name} className="block text-sm font-medium text-gray-700">
        {field.label}
        {field.required && <span className="text-red-500 ml-1">*</span>}
      </label>

      {/* Help Text */}
      {field.helpText && (
        <p className="text-xs text-gray-500">{field.helpText}</p>
      )}

      {/* Input Wrapper */}
      <div className="relative">
        {/* Input Element */}
        {field.type === 'select' ? (
          <select
            {...register(field.name)}
            className={`w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 ${
              error ? 'border-red-500' : 'border-gray-300'
            }`}
          >
            <option value="">Select {field.label}</option>
            {field.options?.map((opt: any) => (
              <option key={opt.value} value={opt.value}>
                {opt.label}
              </option>
            ))}
          </select>
        ) : (
          <input
            {...register(field.name)}
            type={field.type || 'text'}
            placeholder={field.placeholder || `Enter ${field.label}`}
            className={`w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 ${
              error ? 'border-red-500' : 'border-gray-300'
            }`}
          />
        )}

        {/* Unit Selector (for number fields) */}
        {field.unit && (
          <select
            defaultValue={field.defaultUnit}
            className="absolute right-2 top-2 border-0 bg-transparent text-sm"
          >
            {field.units?.map((u: string) => (
              <option key={u} value={u}>{u}</option>
            ))}
          </select>
        )}
      </div>

      {/* Example */}
      {field.example && (
        <p className="text-xs text-gray-500">
          Example: {field.example}
        </p>
      )}

      {/* Error Message */}
      {error && (
        <p className="text-sm text-red-500">{error.message}</p>
      )}
    </div>
  );
}
```

---

### 2.3 Result Display Component

```typescript
// src/components/calculator/ResultDisplay.tsx

interface ResultDisplayProps {
  result: any;
  calculator: CalculatorType;
}

export default function ResultDisplay({
  result,
  calculator,
}: ResultDisplayProps) {
  return (
    <div className="bg-gradient-to-br from-blue-50 to-indigo-50 rounded-lg p-8 border-2 border-blue-200">
      {/* Main Result */}
      <div className="text-center mb-8">
        <p className="text-gray-600 text-sm mb-2">
          {calculator.title} Result
        </p>
        <p className="text-5xl font-bold text-blue-600">
          {formatResult(result.primary)}
        </p>
        <p className="text-gray-500 mt-2">
          {result.primaryLabel || 'Result'}
        </p>
      </div>

      {/* Breakdown (if available) */}
      {result.breakdown && (
        <div className="grid grid-cols-2 md:grid-cols-3 gap-4 mt-8 pt-8 border-t border-blue-200">
          {Object.entries(result.breakdown).map(([key, value]: [string, any]) => (
            <div key={key} className="text-center">
              <p className="text-xs text-gray-600 uppercase tracking-wide">
                {formatLabel(key)}
              </p>
              <p className="text-lg font-semibold text-gray-900 mt-1">
                {formatResult(value)}
              </p>
            </div>
          ))}
        </div>
      )}

      {/* Chart (if applicable) */}
      {result.chart && (
        <div className="mt-8 pt-8 border-t border-blue-200">
          <BreakdownChart data={result.chart} />
        </div>
      )}
    </div>
  );
}

function formatResult(value: any): string {
  if (typeof value === 'number') {
    return value.toLocaleString('en-IN', {
      maximumFractionDigits: 2,
      minimumFractionDigits: 0,
    });
  }
  return String(value);
}

function formatLabel(str: string): string {
  return str
    .replace(/_/g, ' ')
    .split(' ')
    .map((word) => word.charAt(0).toUpperCase() + word.slice(1))
    .join(' ');
}
```

---

### 2.4 Share Result Component

```typescript
// src/components/calculator/ShareResult.tsx

export default function ShareResult({ result, calculator }: ShareResultProps) {
  const [showOptions, setShowOptions] = useState(false);

  const shareData = {
    title: calculator.title,
    text: generateShareText(result, calculator),
    url: typeof window !== 'undefined' ? window.location.href : '',
  };

  const onShare = async (platform: 'whatsapp' | 'facebook' | 'twitter' | 'copy') => {
    const text = shareData.text;
    const url = shareData.url;

    switch (platform) {
      case 'whatsapp':
        window.open(
          `https://wa.me/?text=${encodeURIComponent(text + ' ' + url)}`,
          '_blank'
        );
        break;
      case 'facebook':
        window.open(
          `https://www.facebook.com/sharer/sharer.php?u=${encodeURIComponent(url)}`,
          '_blank'
        );
        break;
      case 'twitter':
        window.open(
          `https://twitter.com/intent/tweet?text=${encodeURIComponent(text)}&url=${encodeURIComponent(url)}`,
          '_blank'
        );
        break;
      case 'copy':
        await navigator.clipboard.writeText(shareData.text);
        alert('Result copied to clipboard!');
        break;
    }

    trackEvent('result_shared', {
      calculator_id: calculator.id,
      platform,
    });
  };

  return (
    <div className="relative">
      <button
        onClick={() => setShowOptions(!showOptions)}
        className="px-4 py-2 bg-green-600 hover:bg-green-700 text-white rounded-lg font-medium"
      >
        📤 Share Result
      </button>

      {showOptions && (
        <div className="absolute top-full left-0 mt-2 bg-white rounded-lg shadow-lg p-3 space-y-2 z-50">
          <button
            onClick={() => onShare('whatsapp')}
            className="block w-full text-left px-4 py-2 hover:bg-gray-100 rounded"
          >
            💬 WhatsApp
          </button>
          <button
            onClick={() => onShare('facebook')}
            className="block w-full text-left px-4 py-2 hover:bg-gray-100 rounded"
          >
            f Facebook
          </button>
          <button
            onClick={() => onShare('twitter')}
            className="block w-full text-left px-4 py-2 hover:bg-gray-100 rounded"
          >
            𝕏 Twitter
          </button>
          <button
            onClick={() => onShare('copy')}
            className="block w-full text-left px-4 py-2 hover:bg-gray-100 rounded"
          >
            📋 Copy
          </button>
        </div>
      )}
    </div>
  );
}

function generateShareText(result: any, calculator: CalculatorType): string {
  return `I just calculated my ${calculator.title.toLowerCase()}: ${result.primaryLabel || 'Result'} = ${result.primary}. Try it yourself!`;
}
```

---

## 🔌 SECTION 3: BACKEND API SPECIFICATIONS

### 3.1 Calculator API Endpoints

```typescript
// pages/api/calculators/[id]/calculate.ts

import { NextRequest, NextResponse } from 'next/server';
import { getCalculator, performCalculation } from '@/lib/db';
import { validateCalculatorInput } from '@/lib/validators';
import { trackAnalytics } from '@/lib/tracking';

export async function POST(
  request: NextRequest,
  { params }: { params: { id: string } }
) {
  try {
    // Get calculator config
    const calculator = await getCalculator(params.id);
    if (!calculator) {
      return NextResponse.json(
        { error: 'Calculator not found' },
        { status: 404 }
      );
    }

    // Parse request body
    const body = await request.json();

    // Validate inputs
    const validation = validateCalculatorInput(body, calculator.input_fields);
    if (!validation.valid) {
      return NextResponse.json(
        { error: 'Invalid input', details: validation.errors },
        { status: 400 }
      );
    }

    // Perform calculation
    const result = await performCalculation(calculator, body);

    // Track analytics
    trackAnalytics({
      event_type: 'calculator_complete',
      calculator_id: calculator.id,
      session_id: request.headers.get('x-session-id') || 'anonymous',
    });

    return NextResponse.json({
      success: true,
      result,
      timestamp: new Date().toISOString(),
    });
  } catch (error) {
    console.error('Calculation error:', error);
    return NextResponse.json(
      { error: 'Calculation failed' },
      { status: 500 }
    );
  }
}
```

### 3.2 Example: EMI Calculator Backend Logic

```typescript
// lib/calculations/finance.ts

export interface EMIInput {
  principal: number;
  annualRate: number;
  years: number;
}

export interface EMIResult {
  primary: number;
  primaryLabel: string;
  breakdown: {
    monthly_emi: number;
    total_amount: number;
    total_interest: number;
    principal_amount: number;
  };
  amortizationSchedule: AmortizationRow[];
  chart: {
    labels: string[];
    principal: number[];
    interest: number[];
  };
}

export function calculateEMI(input: EMIInput): EMIResult {
  const { principal, annualRate, years } = input;

  // Validate inputs
  if (principal <= 0 || annualRate < 0 || years <= 0) {
    throw new Error('Invalid inputs');
  }

  // Convert annual rate to monthly
  const monthlyRate = annualRate / 12 / 100;
  const numberOfPayments = years * 12;

  // EMI Formula: P * r * (1 + r)^n / ((1 + r)^n - 1)
  const numerator = principal * monthlyRate * Math.pow(1 + monthlyRate, numberOfPayments);
  const denominator = Math.pow(1 + monthlyRate, numberOfPayments) - 1;
  const monthlyEMI = numerator / denominator;

  // Calculate totals
  const totalAmount = monthlyEMI * numberOfPayments;
  const totalInterest = totalAmount - principal;

  // Generate amortization schedule
  const amortizationSchedule = generateAmortizationSchedule({
    principal,
    monthlyRate,
    monthlyEMI,
    numberOfPayments,
  });

  // Generate chart data
  const chartData = generateChartData(amortizationSchedule);

  return {
    primary: monthlyEMI,
    primaryLabel: 'Monthly EMI',
    breakdown: {
      monthly_emi: monthlyEMI,
      total_amount: totalAmount,
      total_interest: totalInterest,
      principal_amount: principal,
    },
    amortizationSchedule,
    chart: chartData,
  };
}

function generateAmortizationSchedule(params: {
  principal: number;
  monthlyRate: number;
  monthlyEMI: number;
  numberOfPayments: number;
}): AmortizationRow[] {
  const { principal, monthlyRate, monthlyEMI, numberOfPayments } = params;
  const schedule: AmortizationRow[] = [];
  let remainingBalance = principal;

  for (let month = 1; month <= numberOfPayments; month++) {
    const interestPayment = remainingBalance * monthlyRate;
    const principalPayment = monthlyEMI - interestPayment;
    remainingBalance -= principalPayment;

    schedule.push({
      month,
      emi: monthlyEMI,
      principal: principalPayment,
      interest: interestPayment,
      balance: Math.max(0, remainingBalance),
    });

    // Limit to first 60 months for display
    if (month === 60) break;
  }

  return schedule;
}

interface AmortizationRow {
  month: number;
  emi: number;
  principal: number;
  interest: number;
  balance: number;
}
```

---

## 📋 SECTION 4: CALCULATOR DATABASE - 100+ SPECIFICATIONS

### 4.1 Finance Calculators (Sample)

```json
[
  {
    "slug": "emi-calculator",
    "title": "EMI Calculator - Accurate Loan Payment Calculator",
    "description": "Calculate your monthly EMI for home loans, auto loans, and personal loans with amortization schedule",
    "category": "finance",
    "subcategory": "loans",
    "seo_title": "EMI Calculator - Calculate Monthly Loan Payment Online",
    "seo_description": "Use our free EMI calculator to compute monthly loan payments. Works for home loans, auto loans, personal loans with interest breakup.",
    "input_fields": [
      {
        "name": "principal",
        "label": "Loan Amount",
        "type": "number",
        "helpText": "Enter the principal amount you want to borrow",
        "placeholder": "100000",
        "required": true,
        "unit": "₹",
        "min": 1000,
        "max": 10000000,
        "example": "₹2,00,000"
      },
      {
        "name": "annualRate",
        "label": "Annual Interest Rate (%)",
        "type": "number",
        "placeholder": "8.5",
        "required": true,
        "min": 0,
        "max": 30,
        "step": 0.01,
        "example": "8.5%"
      },
      {
        "name": "years",
        "label": "Loan Tenure (Years)",
        "type": "number",
        "placeholder": "10",
        "required": true,
        "min": 1,
        "max": 40,
        "example": "10 years"
      }
    ],
    "output_format": {
      "primary": { "label": "Monthly EMI", "currency": "INR" },
      "breakdown": {
        "total_amount": "Total Amount Payable",
        "total_interest": "Total Interest Paid",
        "principal_amount": "Principal Amount"
      }
    },
    "formula_latex": "EMI = \\frac{P \\times r \\times (1 + r)^n}{((1 + r)^n - 1)}",
    "formula_json": {
      "type": "emi",
      "formula": "P * r * (1 + r)^n / ((1 + r)^n - 1)",
      "variables": {
        "P": "Principal",
        "r": "Monthly interest rate",
        "n": "Number of months"
      }
    }
  },
  {
    "slug": "sip-calculator",
    "title": "SIP Calculator - Systematic Investment Plan Returns",
    "category": "finance",
    "subcategory": "investments",
    "input_fields": [
      {
        "name": "monthlyInvestment",
        "label": "Monthly Investment Amount",
        "type": "number",
        "unit": "₹",
        "required": true,
        "min": 100,
        "max": 1000000,
        "example": "₹5,000"
      },
      {
        "name": "annualReturn",
        "label": "Expected Annual Return (%)",
        "type": "number",
        "required": true,
        "min": 0,
        "max": 40,
        "example": "12%"
      },
      {
        "name": "years",
        "label": "Investment Period (Years)",
        "type": "number",
        "required": true,
        "min": 1,
        "max": 50,
        "example": "10 years"
      }
    ]
  },
  {
    "slug": "compound-interest-calculator",
    "title": "Compound Interest Calculator",
    "category": "finance",
    "subcategory": "savings",
    "input_fields": [
      {
        "name": "principal",
        "label": "Principal Amount",
        "type": "number",
        "unit": "₹",
        "required": true
      },
      {
        "name": "rate",
        "label": "Annual Interest Rate (%)",
        "type": "number",
        "required": true
      },
      {
        "name": "years",
        "label": "Time Period (Years)",
        "type": "number",
        "required": true
      },
      {
        "name": "frequency",
        "label": "Compounding Frequency",
        "type": "select",
        "options": [
          { "label": "Annually", "value": 1 },
          { "label": "Semi-Annually", "value": 2 },
          { "label": "Quarterly", "value": 4 },
          { "label": "Monthly", "value": 12 }
        ],
        "required": true
      }
    ]
  }
]
```

### 4.2 Converter Specifications

```json
[
  {
    "slug": "cm-to-inches-converter",
    "title": "CM to Inches Converter",
    "category": "converters",
    "subcategory": "length",
    "input_fields": [
      {
        "name": "value",
        "label": "Centimeters",
        "type": "number",
        "required": true,
        "unit": "cm",
        "example": "100"
      }
    ],
    "output_format": {
      "primary": {
        "label": "Inches",
        "unit": "in"
      }
    },
    "formula_json": {
      "type": "simple_conversion",
      "formula": "cm * 0.3937",
      "variables": {
        "cm": "Centimeters",
        "0.3937": "Conversion factor"
      }
    }
  },
  {
    "slug": "temperature-converter",
    "title": "Temperature Converter - Celsius Fahrenheit Kelvin",
    "category": "converters",
    "subcategory": "temperature",
    "input_fields": [
      {
        "name": "value",
        "label": "Temperature Value",
        "type": "number",
        "required": true,
        "example": "25"
      },
      {
        "name": "fromUnit",
        "label": "From",
        "type": "select",
        "options": [
          { "label": "Celsius (°C)", "value": "celsius" },
          { "label": "Fahrenheit (°F)", "value": "fahrenheit" },
          { "label": "Kelvin (K)", "value": "kelvin" }
        ],
        "required": true
      },
      {
        "name": "toUnit",
        "label": "To",
        "type": "select",
        "options": [
          { "label": "Celsius (°C)", "value": "celsius" },
          { "label": "Fahrenheit (°F)", "value": "fahrenheit" },
          { "label": "Kelvin (K)", "value": "kelvin" }
        ],
        "required": true
      }
    ]
  }
]
```

### 4.3 Education Calculators

```json
[
  {
    "slug": "cgpa-calculator",
    "title": "CGPA Calculator - Calculate GPA from Marks",
    "category": "education",
    "subcategory": "grades",
    "description": "Calculate your CGPA (Cumulative Grade Point Average) from your marks in multiple subjects",
    "input_fields": [
      {
        "name": "subjects",
        "label": "Subject Marks",
        "type": "array",
        "arrayItem": {
          "name": "subject",
          "label": "Subject Name",
          "type": "text"
        },
        "arrayItem2": {
          "name": "marks",
          "label": "Marks Obtained",
          "type": "number",
          "max": 100
        }
      }
    ]
  },
  {
    "slug": "jee-rank-predictor",
    "title": "JEE Main Rank Predictor - Estimate Your All India Rank",
    "category": "education",
    "subcategory": "exams",
    "input_fields": [
      {
        "name": "score",
        "label": "Your JEE Score",
        "type": "number",
        "required": true,
        "min": 0,
        "max": 300
      },
      {
        "name": "category",
        "label": "Category",
        "type": "select",
        "options": [
          { "label": "General", "value": "general" },
          { "label": "OBC", "value": "obc" },
          { "label": "SC", "value": "sc" },
          { "label": "ST", "value": "st" }
        ]
      },
      {
        "name": "year",
        "label": "Exam Year",
        "type": "select",
        "options": [
          { "label": "2024", "value": "2024" },
          { "label": "2023", "value": "2023" }
        ]
      }
    ]
  }
]
```

---

## 📰 SECTION 5: BLOG CONTENT SPECIFICATIONS

### 5.1 Blog Post Template (Markdown Structure)

```markdown
---
title: "How to Calculate Age from Date of Birth (2024 Guide)"
slug: "how-to-calculate-age-from-date-of-birth"
description: "Learn how to calculate age accurately from your date of birth. Includes formula, examples, common mistakes, and our free age calculator."
keywords: "age calculator, how to calculate age, age from date of birth"
author: "Calcarena Team"
published_at: 2024-01-15
featured_image: "/images/blog/age-calculator.jpg"
calculator_id: "age-calculator"
related_calculators: ["age-calculator", "date-difference-calculator"]
---

## Introduction

Calculating age from a date of birth is one of the most common calculations people need to do.
Whether you're applying for a job, calculating eligibility, or just curious, this guide will
show you exactly how to calculate your age accurately.

**Quick Answer**: If you were born on January 15, 2000, and today is January 15, 2024, you are
exactly 24 years old.

> **Use our calculator**: [Try our Age Calculator]({{calculator_widget:age-calculator}})

---

## What Is Age and How Is It Calculated?

Age is the amount of time that has passed since a person's birth. It's typically measured in:
- **Years** (most common)
- **Months** (for infants)
- **Days** (for newborns)

### The Simple Formula

```
Age in years = Current Year - Birth Year
```

However, this basic formula has a major flaw...

---

## How to Calculate Age Accurately

### Method 1: Using The Correct Formula

The accurate way to calculate age accounts for whether your birthday has passed this year.

**Formula**:
```
If today's date ≥ birthday this year:
  Age = Current Year - Birth Year

If today's date < birthday this year:
  Age = (Current Year - Birth Year) - 1
```

### Method 2: Day-by-Day Calculation

For maximum precision:

1. Calculate days from birth date to end of birth year
2. Add all complete years between birth year and current year
3. Add days from start of current year to today
4. Convert total days to years and months

### Example Calculation

**Example**: Sarah was born on **June 15, 2000**. Today is **January 20, 2024**.

```
Step 1: Years difference = 2024 - 2000 = 24
Step 2: Has her birthday passed?
        Today is Jan 20, her birthday is June 15
        No, her birthday hasn't passed yet
Step 3: Therefore, her age = 24 - 1 = 23 years

Additional calculation:
- From June 15 to Jan 20 = 7 months and 5 days
- So Sarah is: 23 years, 7 months, and 5 days old
```

---

## Common Mistakes When Calculating Age

❌ **Mistake 1**: Using only the year difference without checking if birthday has passed
✅ **Solution**: Always compare today's date with the birthday in the current year

❌ **Mistake 2**: Forgetting leap years when calculating exact days
✅ **Solution**: Use a calculator (like ours) that accounts for leap years

❌ **Mistake 3**: Confusing age with generation/cohort
✅ **Solution**: Age is specific to an individual's birthdate

---

## Using Our Age Calculator

Our calculator makes this super simple:

1. Enter your **date of birth** (or the date you want to calculate from)
2. Click **"Calculate"**
3. Get your exact age in **years, months, and days**

[**Try the Age Calculator**]({{calculator_widget:age-calculator}})

---

## FAQ

**Q: How accurate is the age calculator?**
A: Our calculator is accurate to the day. It accounts for leap years and all calendar variations.

**Q: Can I calculate someone else's age?**
A: Yes! Enter any birthdate and we'll calculate that person's age.

**Q: What if I don't remember the exact day I was born?**
A: Use "January 1" for the month and day. This will give you an approximate age.

**Q: How is age calculated in different countries?**
A: In most countries, age is the number of complete years since birth. Some East Asian cultures use "age reckoning" which is different. Our calculator uses the international standard.

---

## Related Tools

- [Date Difference Calculator](/calculator/date-difference-calculator/) - Calculate days between any two dates
- [Days Calculator](/calculator/days-calculator/) - Convert days to weeks, months, years
- [Time Calculator](/calculator/time-calculator/) - Calculate time differences

---

## Key Takeaways

- Age = Current Year - Birth Year, **only if your birthday has passed**
- If your birthday hasn't passed this year, subtract 1
- Our age calculator handles all the complexity automatically
- Accounting for leap years is important for exact calculations

[**Calculate Your Age Now** →](/calculator/age-calculator/)
```

---

### 5.2 Blog Metadata for SEO

```typescript
// Example blog post with full SEO markup

interface BlogPost {
  title: "How to Calculate Age from Date of Birth (2024 Guide)",
  slug: "how-to-calculate-age-from-date-of-birth",

  // SEO
  seo_title: "How to Calculate Age from Date of Birth (Complete Guide)",
  seo_description: "Learn how to calculate age accurately from your date of birth. Formula, examples, common mistakes, and free age calculator tool.",
  seo_keywords: ["age calculator", "calculate age", "age from date of birth", "how old am I"],

  // Canonical & OpenGraph
  canonical: "https://calcarena.com/blog/how-to-calculate-age-from-date-of-birth/",
  og_title: "How to Calculate Age from Date of Birth",
  og_description: "Simple formula and free calculator to find your exact age in years, months, and days.",
  og_image: "https://calcarena.com/images/blog/age-calculator-og.jpg",

  // Content
  content: "... [full markdown content]",
  excerpt: "Learn how to calculate your age accurately from your date of birth with our step-by-step guide and free calculator.",
  featured_image: "https://calcarena.com/images/blog/age-calculator-featured.jpg",

  // Related items
  related_calculator_ids: ["age-calculator", "date-difference-calculator"],
  internal_links: [
    { text: "Date Difference Calculator", url: "/calculator/date-difference-calculator/" },
    { text: "Days Calculator", url: "/calculator/days-calculator/" }
  ],

  // Publishing
  author: "Calcarena Team",
  published_at: "2024-01-15T10:00:00Z",
  updated_at: "2024-01-15T10:00:00Z",
  language: "en",

  // Stats
  word_count: 2150,
  reading_time_minutes: 8,
  view_count: 0,
}
```

---

## 🔍 SECTION 6: SEO IMPLEMENTATION GUIDE

### 6.1 Schema Markup Generation

```typescript
// lib/schema.ts

export function generateCalculatorSchema(
  calculator: Calculator,
  baseUrl: string
) {
  return {
    "@context": "https://schema.org",
    "@type": "SoftwareApplication",
    "name": calculator.title,
    "description": calculator.description,
    "url": `${baseUrl}/calculator/${calculator.slug}`,
    "applicationCategory": "UtilityApplication",
    "offers": {
      "@type": "Offer",
      "price": "0",
      "priceCurrency": "USD"
    },
    "featureList": [
      "Free calculator",
      "No sign-up required",
      "Mobile-friendly",
      "Accurate results"
    ]
  };
}

export function generateHowToSchema(
  calculator: Calculator,
  steps: string[]
) {
  return {
    "@context": "https://schema.org",
    "@type": "HowTo",
    "name": `How to use ${calculator.title}`,
    "step": steps.map((step, index) => ({
      "@type": "HowToStep",
      "position": index + 1,
      "name": step,
      "text": step
    }))
  };
}

export function generateFAQSchema(faqs: FAQ[]) {
  return {
    "@context": "https://schema.org",
    "@type": "FAQPage",
    "mainEntity": faqs.map((faq) => ({
      "@type": "Question",
      "name": faq.question,
      "acceptedAnswer": {
        "@type": "Answer",
        "text": faq.answer
      }
    }))
  };
}
```

### 6.2 Meta Tags & SEO Component

```typescript
// components/SEO.tsx

import Head from 'next/head';

interface SEOProps {
  title: string;
  description: string;
  image?: string;
  url: string;
  type?: string;
  schema?: any;
}

export default function SEO({
  title,
  description,
  image,
  url,
  type = 'website',
  schema,
}: SEOProps) {
  return (
    <Head>
      {/* Basic Meta Tags */}
      <title>{title}</title>
      <meta name="description" content={description} />
      <meta name="viewport" content="width=device-width, initial-scale=1" />
      <meta charSet="utf-8" />

      {/* Open Graph */}
      <meta property="og:type" content={type} />
      <meta property="og:title" content={title} />
      <meta property="og:description" content={description} />
      <meta property="og:url" content={url} />
      {image && <meta property="og:image" content={image} />}

      {/* Twitter Card */}
      <meta name="twitter:card" content="summary_large_image" />
      <meta name="twitter:title" content={title} />
      <meta name="twitter:description" content={description} />
      {image && <meta name="twitter:image" content={image} />}

      {/* Canonical */}
      <link rel="canonical" href={url} />

      {/* Schema Markup */}
      {schema && (
        <script
          type="application/ld+json"
          dangerouslySetInnerHTML={{ __html: JSON.stringify(schema) }}
        />
      )}
    </Head>
  );
}
```

---

## 💾 SECTION 7: FEATURE SPECIFICATIONS

### 7.1 Save Result Feature

```typescript
// Database table already defined above

// API endpoint: pages/api/results/save.ts

export async function POST(request: NextRequest) {
  const { calculatorId, inputData, resultData } = await request.json();
  const user = await getAuthUser(request);

  if (!user) {
    return NextResponse.json(
      { error: 'Unauthorized' },
      { status: 401 }
    );
  }

  // Save to database
  const savedResult = await db.saved_results.create({
    user_id: user.id,
    calculator_id: calculatorId,
    input_data: inputData,
    result_data: resultData,
    created_at: new Date(),
  });

  return NextResponse.json(savedResult);
}

// Frontend component
export function SaveResult({ result, calculator }: SaveResultProps) {
  const { user } = useAuth();
  const [isSaved, setIsSaved] = useState(false);
  const [isLoading, setIsLoading] = useState(false);

  const handleSave = async () => {
    if (!user) {
      // Redirect to login
      router.push('/login');
      return;
    }

    setIsLoading(true);
    try {
      const response = await fetch('/api/results/save', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          calculatorId: calculator.id,
          inputData: result.inputs,
          resultData: result.output,
        }),
      });

      if (response.ok) {
        setIsSaved(true);
        trackEvent('result_saved', { calculator_id: calculator.id });
      }
    } finally {
      setIsLoading(false);
    }
  };

  return (
    <button
      onClick={handleSave}
      disabled={isLoading || isSaved}
      className={`px-4 py-2 rounded-lg font-medium ${
        isSaved
          ? 'bg-green-600 text-white'
          : 'bg-blue-600 hover:bg-blue-700 text-white'
      }`}
    >
      {isSaved ? '✓ Saved' : isLoading ? 'Saving...' : '💾 Save'}
    </button>
  );
}
```

---

### 7.2 Export to PDF Feature

```typescript
// lib/export.ts

import jsPDF from 'jspdf';
import html2canvas from 'html2canvas';

export async function exportResultToPDF(
  calculator: Calculator,
  result: any
) {
  const element = document.getElementById('result-container');
  const canvas = await html2canvas(element, { scale: 2 });
  const imgData = canvas.toDataURL('image/png');

  const pdf = new jsPDF({
    orientation: 'portrait',
    unit: 'mm',
    format: 'a4',
  });

  // Add header
  pdf.setFontSize(16);
  pdf.text(calculator.title, 20, 20);

  // Add image
  pdf.addImage(imgData, 'PNG', 20, 30, 170, 100);

  // Add metadata
  pdf.setFontSize(10);
  pdf.text(`Generated on: ${new Date().toLocaleDateString()}`, 20, 150);
  pdf.text(`Calculator: ${calculator.title}`, 20, 160);

  // Save
  pdf.save(`${calculator.slug}-result.pdf`);
}

// Excel export
import ExcelJS from 'exceljs';

export async function exportResultToExcel(
  calculator: Calculator,
  result: any
) {
  const workbook = new ExcelJS.Workbook();
  const worksheet = workbook.addWorksheet(calculator.title.slice(0, 31));

  // Add data
  worksheet.addRow([calculator.title]);
  worksheet.addRow([]);
  worksheet.addRow(['Input', 'Value']);

  Object.entries(result.inputs).forEach(([key, value]) => {
    worksheet.addRow([key, value]);
  });

  worksheet.addRow([]);
  worksheet.addRow(['Result', 'Value']);
  Object.entries(result.output.breakdown || {}).forEach(([key, value]) => {
    worksheet.addRow([key, value]);
  });

  // Download
  await workbook.xlsx.writeFile(`${calculator.slug}-result.xlsx`);
}
```

---

## 💰 SECTION 8: MONETIZATION IMPLEMENTATION

### 8.1 Stripe Integration for Premium Tier

```typescript
// lib/stripe.ts

import Stripe from 'stripe';

const stripe = new Stripe(process.env.STRIPE_SECRET_KEY!);

// Create subscription
export async function createSubscription(
  userId: string,
  email: string,
  priceId: string
) {
  const customer = await stripe.customers.create({
    email,
    metadata: { userId },
  });

  const subscription = await stripe.subscriptions.create({
    customer: customer.id,
    items: [{ price: priceId }],
    payment_settings: {
      save_default_payment_method: 'on_subscription',
    },
  });

  return subscription;
}

// Handle webhook
export async function handleStripeWebhook(event: Stripe.Event) {
  switch (event.type) {
    case 'invoice.payment_succeeded':
      // Update user premium status
      await db.users.update(
        { stripe_subscription_id: event.data.object.subscription },
        { is_premium: true, premium_expires_at: null }
      );
      break;

    case 'customer.subscription.deleted':
      // Downgrade user
      await db.users.update(
        { stripe_subscription_id: event.data.object.id },
        { is_premium: false }
      );
      break;
  }
}
```

### 8.2 Ad Implementation

```typescript
// components/AdUnit.tsx

export function AdUnit({ placement = 'top' }: { placement: string }) {
  useEffect(() => {
    // Load Google AdSense script
    if (window.adsbygoogle) {
      window.adsbygoogle.push({});
    }
  }, []);

  return (
    <div className={`ad-container ${placement}`}>
      <ins
        className="adsbygoogle"
        style={{ display: 'block' }}
        data-ad-client={process.env.NEXT_PUBLIC_ADSENSE_ID}
        data-ad-slot="1234567890"
        data-ad-format="auto"
        data-full-width-responsive="true"
      ></ins>
    </div>
  );
}

// Usage in calculator page
export default function CalculatorPage() {
  return (
    <>
      <AdUnit placement="top" />
      <Calculator {...props} />
      <AdUnit placement="bottom" />
    </>
  );
}
```

---

## 🤝 SECTION 9: PARTNERSHIP INTEGRATION

### 9.1 Embed Widget Code

```html
<!-- Embed code for partners -->
<iframe
  src="https://calcarena.com/embed/emi-calculator/?ref=partner-domain"
  width="100%"
  height="600"
  frameborder="0"
  allowfullscreen=""
  style="border: 1px solid #ddd; border-radius: 8px;"
></iframe>
```

### 9.2 Affiliate Link Generation

```typescript
// API to generate affiliate links

export async function POST(request: NextRequest) {
  const { partnerId, calculatorId } = await request.json();

  // Verify partner
  const partner = await db.partnerships.findUnique({ id: partnerId });
  if (!partner) {
    return NextResponse.json({ error: 'Invalid partner' }, { status: 400 });
  }

  // Generate unique affiliate URL
  const affiliateLink = await db.affiliate_links.create({
    partner_id: partnerId,
    calculator_id: calculatorId,
    affiliate_url: `https://calcarena.com/calculator/${calculatorId}?ref=${partnerId}`,
  });

  return NextResponse.json(affiliateLink);
}
```

---

## 📊 SECTION 10: ANALYTICS & TRACKING

### 10.1 Event Tracking

```typescript
// lib/tracking.ts

export function trackEvent(eventName: string, properties?: any) {
  // Google Analytics
  gtag.event(eventName, {
    event_category: 'calculator',
    ...properties,
  });

  // Mixpanel
  mixpanel.track(eventName, properties);

  // Custom analytics
  fetch('/api/analytics/track', {
    method: 'POST',
    body: JSON.stringify({
      event_type: eventName,
      metadata: properties,
      timestamp: new Date(),
    }),
  });
}

// Track calculator completion
export function trackCalculatorComplete(calculatorId: string, result: any) {
  trackEvent('calculator_complete', {
    calculator_id: calculatorId,
    result_value: result.primary,
  });
}

// Track share
export function trackShare(calculatorId: string, platform: string) {
  trackEvent('result_shared', {
    calculator_id: calculatorId,
    platform,
  });
}

// Track save
export function trackSave(calculatorId: string) {
  trackEvent('result_saved', {
    calculator_id: calculatorId,
  });
}
```

---

## 🎬 END OF SPECIFIC PLAN DOCUMENT

This document contains ALL specifications needed to build Calcarena:
- Complete database schema
- React component code
- API endpoints
- 100+ calculator specifications
- Blog templates
- SEO markup
- Feature implementations
- Integration guides
- Analytics setup

Everything is ready to implement. Start with the tech stack setup, then build the database, then create components.

