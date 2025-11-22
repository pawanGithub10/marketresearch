# 🔥 ACTION DOCUMENT: CALCULATOR WEBSITE - 90-DAY EXECUTION
**Day-by-Day, Task-by-Task Implementation Guide**

---

## 📋 QUICK START

| Phase | Duration | Owner | Status | Budget |
|-------|----------|-------|--------|--------|
| **Phase 1: Setup** | Days 1-7 | Tech Lead | 🟢 Ready | $0 (internal) |
| **Phase 2: Core Build** | Days 8-21 | Dev Team | 🔴 Not Started | $2-5K (hosting) |
| **Phase 3: Launch Prep** | Days 22-28 | Marketing + Dev | 🔴 Not Started | $500-1K |
| **Phase 4: Soft Launch** | Days 29-42 | Full Team | 🔴 Not Started | $1-2K |
| **Phase 5: Scale & Distribution** | Days 43-56 | Marketing Lead | 🔴 Not Started | $2-5K |
| **Phase 6: Monetization** | Days 57-90 | Growth Lead | 🔴 Not Started | $3-5K |

**Total Budget (90 days)**: $8-18K

---

## ⚡ PHASE 1: SETUP & INFRASTRUCTURE (Days 1-7)

### **DAY 1: Project Kickoff**

#### Morning (2 hours)
- [ ] **Tech Lead**: Review strategy document (CALCULATOR_MARKETING_STRATEGY.md)
- [ ] **Project Manager**: Create Asana/Linear board with all tasks
- [ ] **All**: Team standup (1 hour) - assign roles, review timeline

#### Roles Assignment
| Role | Responsibility | Person | Contact |
|------|---|---|---|
| **Tech Lead** | Infrastructure, database, API, performance | [Name] | [Email] |
| **Dev Lead** | Calculator building, code quality, testing | [Name] | [Email] |
| **Content Lead** | Blog writing, SEO optimization, copywriting | [Name] | [Email] |
| **Marketing Lead** | Social media, partnerships, ads | [Name] | [Email] |
| **Product Manager** | UX/UI, feature prioritization, user testing | [Name] | [Email] |
| **Growth Lead** | Analytics, monetization, KPIs | [Name] | [Email] |

#### Afternoon (2 hours)
- [ ] **Tech Lead**: Set up project repository (Git structure)
- [ ] **Tech Lead**: Choose tech stack (Recommendation: Next.js + TypeScript + Supabase)
- [ ] **Project Manager**: Create GitHub/Asana project board

**Deliverable**: Project board setup with 200+ tasks

---

### **DAY 2: Infrastructure & Tech Setup**

#### Morning (3 hours)
- [ ] **Tech Lead**: Register domain (if not done): Calcarena.com or similar
- [ ] **Tech Lead**: Set up hosting (Vercel, Cloudflare, AWS)
- [ ] **Tech Lead**: Configure DNS + SSL certificate
- [ ] **Tech Lead**: Set up GitHub repository with branch protection rules

**Command Checklist**:
```bash
# Initialize repo
git init calcarena
cd calcarena
git branch -b main

# Create .gitignore
echo "node_modules/
.env.local
.next/
dist/
.DS_Store" > .gitignore

# Set up folder structure
mkdir -p {src/components,src/pages,src/calculators,src/blogs,src/styles,public/images,database}
```

#### Afternoon (3 hours)
- [ ] **Tech Lead**: Set up Next.js project
- [ ] **Tech Lead**: Configure database (PostgreSQL or Firebase)
- [ ] **Tech Lead**: Set up environment variables
- [ ] **Tech Lead**: Test local dev environment

**Tech Stack Recommendation**:
```
Frontend: Next.js 14 (React)
Database: PostgreSQL (Supabase)
Auth: Supabase Auth (free tier)
Hosting: Vercel
CDN: Cloudflare
Analytics: Google Analytics 4 + Mixpanel
```

**Deliverable**: Live dev environment + repository ready

---

### **DAY 3: Database & Calculator Framework**

#### Morning (3 hours)
- [ ] **Tech Lead**: Design database schema
  ```sql
  -- Calculators table
  CREATE TABLE calculators (
    id UUID PRIMARY KEY,
    slug VARCHAR(255) UNIQUE,
    title VARCHAR(255),
    description TEXT,
    category VARCHAR(50),
    formula TEXT,
    input_fields JSONB,
    created_at TIMESTAMP,
    updated_at TIMESTAMP
  );

  -- Blog posts table
  CREATE TABLE blog_posts (
    id UUID PRIMARY KEY,
    slug VARCHAR(255) UNIQUE,
    title VARCHAR(255),
    content TEXT,
    calculator_id UUID REFERENCES calculators(id),
    published_at TIMESTAMP,
    created_at TIMESTAMP
  );

  -- User accounts table
  CREATE TABLE users (
    id UUID PRIMARY KEY,
    email VARCHAR(255) UNIQUE,
    created_at TIMESTAMP
  );

  -- User saved results
  CREATE TABLE saved_results (
    id UUID PRIMARY KEY,
    user_id UUID REFERENCES users(id),
    calculator_id UUID REFERENCES calculators(id),
    result_data JSONB,
    created_at TIMESTAMP
  );
  ```

- [ ] **Dev Lead**: Create calculator component template (React)
  ```typescript
  // src/components/Calculator.tsx
  interface CalculatorConfig {
    title: string;
    slug: string;
    inputs: InputField[];
    formula: (inputs: any) => number;
    resultLabel: string;
  }

  export function Calculator({ config }: { config: CalculatorConfig }) {
    const [inputs, setInputs] = useState({});
    const [result, setResult] = useState<number | null>(null);

    const handleCalculate = () => {
      const result = config.formula(inputs);
      setResult(result);
    };

    return (
      <div className="calculator">
        {/* Input fields */}
        {/* Result display */}
        {/* Share button */}
      </div>
    );
  }
  ```

#### Afternoon (3 hours)
- [ ] **Dev Lead**: Build reusable calculator template (80% of work is template, 20% is data)
- [ ] **Dev Lead**: Create API routes for calculations
- [ ] **Test Lead**: Set up unit tests

**Deliverable**: Database schema + calculator template component

---

### **DAY 4: SEO Infrastructure & Schema Setup**

#### Morning (3 hours)
- [ ] **Tech Lead**: Implement schema markup helper function
  ```typescript
  // src/lib/schema.ts
  export function generateCalculatorSchema(calc: Calculator) {
    return {
      "@context": "https://schema.org",
      "@type": "SoftwareApplication",
      name: calc.title,
      description: calc.description,
      applicationCategory: "UtilityApplication",
      offers: {
        "@type": "Offer",
        price: "0",
        priceCurrency: "USD"
      }
    };
  }
  ```

- [ ] **Tech Lead**: Set up Next.js SEO plugin (next-seo)
- [ ] **Content Lead**: Create SEO metadata templates

#### Afternoon (3 hours)
- [ ] **Tech Lead**: Set up Google Analytics 4
- [ ] **Tech Lead**: Set up Search Console + verify domain
- [ ] **Tech Lead**: Create robots.txt and sitemap generation
- [ ] **Content Lead**: Write 10 meta description templates

**Deliverable**: SEO infrastructure ready, Analytics configured

---

### **DAY 5: Design System & UI Components**

#### Morning (3 hours)
- [ ] **Product Manager**: Create design system (colors, typography, spacing)
- [ ] **Product Manager**: Design calculator card component
- [ ] **Dev Lead**: Implement Tailwind CSS configuration

**Color Scheme**:
```css
Primary: #3B82F6 (Blue - trust, clarity)
Secondary: #10B981 (Green - positive, results)
Accent: #F59E0B (Amber - warning, highlight)
Neutral: #F3F4F6 (Light gray - background)
Text: #1F2937 (Dark gray - readability)
```

#### Afternoon (3 hours)
- [ ] **Product Manager**: Design mobile-first layouts
- [ ] **Dev Lead**: Build responsive components (Input, Button, Card, Modal)
- [ ] **Dev Lead**: Test on mobile devices (iOS + Android)

**Deliverable**: Design system + reusable components

---

### **DAY 6: API & Integration Layer**

#### Morning (3 hours)
- [ ] **Dev Lead**: Build calculator API endpoints
  ```typescript
  // pages/api/calculators/[slug].ts
  export default async function handler(req, res) {
    const { slug } = req.query;
    const calc = await db.calculators.findOne({ slug });
    return res.json(calc);
  }

  // pages/api/calculate.ts
  export default async function handler(req, res) {
    const { calculatorId, inputs } = req.body;
    const calc = await db.calculators.findOne({ id: calculatorId });
    const result = calc.formula(inputs);
    return res.json({ result, timestamp: new Date() });
  }
  ```

- [ ] **Dev Lead**: Build user authentication API
- [ ] **Dev Lead**: Build save results API

#### Afternoon (3 hours)
- [ ] **Dev Lead**: Test all APIs with Postman
- [ ] **Dev Lead**: Set up rate limiting
- [ ] **Dev Lead**: Document API endpoints

**Deliverable**: Working API endpoints + documentation

---

### **DAY 7: Testing & Deployment Setup**

#### Morning (3 hours)
- [ ] **QA Lead**: Set up testing framework (Jest + React Testing Library)
- [ ] **QA Lead**: Create test for calculator template
- [ ] **QA Lead**: Set up CI/CD pipeline (GitHub Actions)

#### Afternoon (3 hours)
- [ ] **Tech Lead**: Set up staging environment
- [ ] **Tech Lead**: Deploy to staging
- [ ] **All**: Test on staging environment
- [ ] **Tech Lead**: Document deployment process

**Deliverable**: Staging environment live, CI/CD pipeline working

**END OF PHASE 1**:
- ✅ Repository set up
- ✅ Database configured
- ✅ Tech stack ready
- ✅ SEO infrastructure in place
- ✅ APIs working

---

## 🏗️ PHASE 2: CORE CALCULATOR BUILD (Days 8-21)

### **DAY 8-9: Top 20 High-Priority Calculators**

#### Priority Tier 1 (Days 8-9):
These calculators have highest monthly search volume + lowest KD

| # | Calculator | Search Vol. | Estimated Traffic | Days |
|---|-----------|---|---|---|
| 1 | Age Calculator | 80K | 500/day | 1 |
| 2 | EMI Calculator | 110K | 650/day | 1 |
| 3 | Percentage Calculator | 90K | 550/day | 1 |
| 4 | CGPA Calculator | 75K | 450/day | 1 |
| 5 | Temperature Converter | 98K | 600/day | 0.5 |
| 6 | CM to Inches | 120K | 750/day | 0.5 |
| 7 | KG to LBS | 110K | 650/day | 0.5 |
| 8 | Loan Calculator | 85K | 500/day | 1 |
| 9 | Grade Calculator | 60K | 350/day | 1 |
| 10 | BMI Calculator | 95K | 580/day | 1 |

#### Task Breakdown (Days 8-9):
- [ ] **Dev 1**: Build Age Calculator (Day 8, 4 hours)
  - Input: Date of birth
  - Output: Age in years, months, days
  - Features: Show formatted date, share button

- [ ] **Dev 2**: Build EMI Calculator (Day 8, 4 hours)
  - Inputs: Principal, interest rate, tenure
  - Output: EMI, total interest, total amount
  - Features: Amortization table, downloadable schedule

- [ ] **Dev 3**: Build Percentage Calculator (Day 8, 4 hours)
  - Inputs: Percentage, of amount
  - Output: Result, percentage change options
  - Features: Multiple calculation types

- [ ] **Dev 1**: Build CGPA Calculator (Day 9, 4 hours)
- [ ] **Dev 2**: Build Temperature Converter (Day 9, 2 hours)
- [ ] **Dev 3**: Build CM to Inches Converter (Day 9, 2 hours)

**Definition of Done**:
- ✅ Calculator logic tested
- ✅ Input validation working
- ✅ Mobile responsive
- ✅ Schema markup added
- ✅ Meta tags configured
- ✅ Share button functional
- ✅ Deployed to staging

**Deliverable**: 10 calculators live on staging

---

### **DAY 10-14: Next 30 Calculators (Converters + Education)**

#### Day 10 (Converters - 5 calculators):
- [ ] Meters to Feet
- [ ] Miles to Kilometers
- [ ] Liters to Gallons
- [ ] Grams to Ounces
- [ ] Celsius to Fahrenheit (duplicate but essential)

#### Day 11 (Math & Finance - 5 calculators):
- [ ] Simple Interest
- [ ] Compound Interest
- [ ] Discount Calculator
- [ ] Profit Margin
- [ ] ROI Calculator

#### Day 12 (Health & Education - 5 calculators):
- [ ] SGPA Calculator
- [ ] GPA Calculator
- [ ] Ideal Weight Calculator
- [ ] Daily Calorie Intake
- [ ] Unit Conversion (general)

#### Day 13 (Time & Date - 5 calculators):
- [ ] Date Difference Calculator
- [ ] Days Calculator
- [ ] Time Calculator
- [ ] Hours to Minutes
- [ ] Week Number Calculator

#### Day 14 (Finance Continued - 5 calculators):
- [ ] Salary Calculator
- [ ] Income Tax Calculator
- [ ] GST Calculator
- [ ] FD Calculator
- [ ] RD Calculator

**Daily Workflow (Days 10-14)**:
```
9 AM - 10 AM: Sprint planning (which 5 calc)
10 AM - 12 PM: Dev 1 builds 2 calculators
12 PM - 2 PM: Dev 2 builds 2 calculators
2 PM - 3 PM: Dev 3 builds 1 calculator
3 PM - 4 PM: QA testing all 5
4 PM - 5 PM: Deployment + fixes
```

**Deliverable**: 40 calculators total (10 + 30)

---

### **DAY 15-18: Remaining 60 Calculators (Batched)**

#### Strategy: Template-Driven Build
Since we have template, building becomes FAST

**Formula for Speed**:
1. Create CSV with calculator data (formula, inputs, outputs)
2. Parse CSV → Generate React components
3. Test automatically
4. Deploy in batches

#### CSV Template Example:
```csv
slug,title,description,category,formula,inputs,output
age-calculator,Age Calculator,Calculate your age from DOB,time,"(today - dob) / 365.25","date_of_birth","age_years,age_months,age_days"
percentage,Percentage Calculator,Calculate percentage of amount,math,"(percentage/100) * amount","percentage,amount","result"
```

**Day 15 (Batch 1 - 15 calculators)**:
- [ ] Create CSV with 15 calculators
- [ ] Build generator script
- [ ] Generate components
- [ ] Test & deploy

**Day 16 (Batch 2 - 15 calculators)**:
- [ ] Repeat process
- [ ] Fix any bugs from Batch 1

**Day 17 (Batch 3 - 15 calculators)**:
- [ ] Repeat process

**Day 18 (Batch 4 - 15 calculators + buffer)**:
- [ ] Remaining calculators
- [ ] Testing & optimization

**Deliverable**: 100 calculators live (10 + 30 + 60)

---

### **DAY 19-21: Polish & Optimization**

#### Day 19: Content & Meta Tags
- [ ] **Content Lead**: Write 100 meta descriptions
- [ ] **Content Lead**: Write 100 short descriptions
- [ ] **Content Lead**: Add formulas & explanations to each

#### Day 20: Performance Optimization
- [ ] **Tech Lead**: Optimize images (WebP, lazy loading)
- [ ] **Tech Lead**: Minify CSS/JS
- [ ] **Tech Lead**: Implement caching
- [ ] **Tech Lead**: Run Lighthouse test
- [ ] Goal: **LCP < 2.5s, INP < 75ms, CLS < 0.1**

#### Day 21: QA & Testing
- [ ] **QA Lead**: Test all 100 calculators on mobile
- [ ] **QA Lead**: Test all 100 on desktop
- [ ] **QA Lead**: Test accessibility (WCAG 2.1 AA)
- [ ] **QA Lead**: Test on slow 3G (throttled)
- [ ] **Dev**: Fix any critical issues

**Deliverable**: 100 polished calculators, production-ready

**END OF PHASE 2**:
- ✅ 100 calculators built & tested
- ✅ All pages have schema markup
- ✅ Core Web Vitals optimized
- ✅ Mobile-first design implemented
- ✅ SEO metadata completed

---

## 📰 PHASE 3: CONTENT BUILD (Days 22-28)

### **DAY 22-23: Blog Infrastructure & Templates**

#### Day 22 (3 hours):
- [ ] **Content Lead**: Create blog template (markdown-based)
- [ ] **Content Lead**: Set up blog CMS (optional: Sanity.io or Strapi)
- [ ] **Dev Lead**: Build blog page component
- [ ] **Dev Lead**: Build blog listing page
- [ ] **Dev Lead**: Set up blog pagination

#### Day 23 (3 hours):
- [ ] **Content Lead**: Create blog post template (outline structure)
  ```markdown
  # [KEYWORD] - Complete Guide

  ## Introduction
  - Hook (30 words)
  - Problem statement
  - Solution overview

  ## What is [KEYWORD]?
  - Definition
  - Real-world example
  - Common misconceptions

  ## How to Calculate [KEYWORD]
  - Formula
  - Step-by-step instructions
  - Worked example

  ## Calculator Tool
  [Embed calculator widget here]

  ## Common Mistakes
  - Mistake 1
  - Mistake 2

  ## FAQ
  - Q1
  - Q2
  - Q3

  ## Related Topics
  [Link to related blog posts & calculators]
  ```

- [ ] **Content Lead**: Create SEO checklist for blog posts
- [ ] **Dev Lead**: Test blog RSS feed

**Deliverable**: Blog infrastructure ready

---

### **DAY 24-25: Write First 10 Blogs**

#### Priority Blogs (High Volume, Low KD):

| # | Title | Est. Traffic | Est. KD | Writer | Deadline |
|---|---|---|---|---|---|
| 1 | How to Calculate Age from Date of Birth | 500/day | 12% | Writer A | Day 24 |
| 2 | How to Calculate Percentage (3 Methods) | 400/day | 10% | Writer A | Day 24 |
| 3 | How to Calculate EMI for Home Loan | 350/day | 15% | Writer B | Day 24 |
| 4 | How to Calculate CGPA from Marks | 300/day | 12% | Writer C | Day 24 |
| 5 | How to Calculate Compound Interest | 300/day | 12% | Writer B | Day 25 |
| 6 | How to Convert Temperature (C to F) | 250/day | 12% | Writer A | Day 25 |
| 7 | How to Calculate Discount Percentage | 250/day | 10% | Writer C | Day 25 |
| 8 | How to Calculate Salary Take-Home | 280/day | 18% | Writer B | Day 25 |
| 9 | How to Calculate BMI & Ideal Weight | 300/day | 14% | Writer A | Day 25 |
| 10 | How to Calculate Simple Interest | 250/day | 10% | Writer C | Day 25 |

**Writing Instructions for Each Blog**:
1. **Length**: 1,500-2,000 words
2. **Structure**: Follow template above
3. **Keywords**: Use NLP tool (SEMrush/Ahrefs) to find LSI keywords
4. **Calculator Link**: Embed 2-3 relevant calculators
5. **Internal Links**: Link to 3-5 related blog posts
6. **CTA**: "Try our calculator" at end
7. **Meta Tags**: Write unique meta description (160 chars)
8. **Schema**: Add FAQ + HowTo schema

**Day 24 Activity**:
- Writer A: Blog 1, 2 (4 hours)
- Writer B: Blog 3, 5 (4 hours)
- Writer C: Blog 4, 10 (4 hours)

**Day 25 Activity**:
- Writer A: Blog 6, 9 (4 hours)
- Writer B: Blog 5, 8 (4 hours)
- Writer C: Blog 7 (2 hours) + editing (2 hours)

**Deliverable**: 10 published blog posts

---

### **DAY 26-27: Write Next 20 Blogs**

**Strategy**: Parallel writing (all writers working simultaneously)

| Writer | Day 26 Blogs | Day 27 Blogs | Total |
|--------|---|---|---|
| Writer A | 7 blogs | 7 blogs | 14 |
| Writer B | 7 blogs | 7 blogs | 14 |
| Writer C | 6 blogs | 6 blogs | 12 |
| Editor | Review + format | Review + format | - |

**Blog Ideas for Days 26-27** (sorted by volume):

```
Day 26:
1. How to Calculate Income Tax in India (95K volume)
2. How to Calculate Loan EMI with Extra Payments (6K volume)
3. How to Calculate ROI on Investment (38K volume)
4. How to Calculate Body Fat Percentage (22K volume)
5. How to Calculate SGPA from Marks (12K volume)
6. How to Calculate Grade Point Average (GPA) (65K volume)
7. How to Calculate Markup & Margin (14K volume)

Day 27:
8. How to Calculate Break-Even Point (15K volume)
9. How to Convert Kilometers to Miles (80K volume)
10. How to Calculate Daily Calorie Intake (28K volume)
11. How to Calculate Property Tax (22K volume)
12. How to Calculate Profit Margin (20K volume)
13. How to Calculate Weight Converter (88K volume)
14. How to Calculate Time Difference (28K volume)
15. How to Calculate Pregnancy Due Date (35K volume)
16. How to Convert Currency Exchange Rate (95K volume)
```

**Deliverable**: 30 blog posts total (10 + 20)

---

### **DAY 28: Blog Publishing & Linking**

#### Morning (3 hours):
- [ ] **Editor**: Final review of all 30 blogs
- [ ] **Editor**: Add images to each blog (1-2 images per blog)
- [ ] **Editor**: Publish all 30 blogs to blog section
- [ ] **Content Lead**: Add internal links between related blogs
- [ ] **Content Lead**: Link blogs to relevant calculators

#### Afternoon (3 hours):
- [ ] **Tech Lead**: Update sitemap with blog URLs
- [ ] **Tech Lead**: Submit blogs to Google Search Console
- [ ] **Content Lead**: Create social media captions (30)
- [ ] **QA Lead**: Test all blog pages on mobile

**Deliverable**: 30 published, linked blog posts

**END OF PHASE 3**:
- ✅ 100 calculators with full pages
- ✅ 30 blog posts published
- ✅ All pages SEO-optimized
- ✅ Internal linking complete
- ✅ Ready for soft launch

---

## 🚀 PHASE 4: SOFT LAUNCH & PARTNERSHIPS (Days 29-42)

### **DAY 29-30: Soft Launch to Staging**

#### Day 29 (Full Day):
- [ ] **Tech Lead**: Final performance audit
  - Run Lighthouse test (target: 90+)
  - Run PageSpeed test
  - Test Core Web Vitals
  - Load testing (simulate 1000 concurrent users)

- [ ] **QA Lead**: Final full regression test
  - Test all 100 calculators
  - Test all 30 blog posts
  - Test responsiveness (10+ devices)
  - Test navigation & search

#### Day 30 (Full Day):
- [ ] **All**: Beta user testing (invite 50 friends/colleagues)
  - Share staging link
  - Collect feedback via Google Form
  - Track issues
  - Fix critical bugs
  - Test on real devices (iOS, Android, various desktop)

**Feedback Form Template**:
```
1. Which calculator did you use?
2. Was the interface easy to use? (1-5)
3. Did you find the information helpful? (1-5)
4. What would improve this?
5. Would you recommend this to a friend? (1-5)
6. Found any bugs? Describe:
```

**Deliverable**: Soft launch complete, feedback collected

---

### **DAY 31: Production Deployment**

#### Full Day:
- [ ] **Tech Lead**: Deploy to production (at 9 AM IST)
  - Deploy code
  - Database migration
  - CDN cache clear
  - Monitor uptime

- [ ] **Growth Lead**: Monitor first 24 hours
  - Check error logs
  - Monitor server performance
  - Watch user analytics
  - Respond to immediate issues

- [ ] **Marketing**: Announce launch (if applicable)
  - Email to team
  - Social posts (soft announcement)

**Deliverable**: Calcarena.com live in production

---

### **DAY 32-35: Partnership Outreach - Schools (4 days)**

#### Target: 50 Schools by Day 35

**Outreach Strategy**:
- [ ] **Marketing Lead**: Create list of 500 schools (by state/city)
- [ ] **Marketing Lead**: Personalize outreach email (500 emails)
- [ ] **Growth Lead**: Track open rates & responses
- [ ] **Sales Rep**: Schedule demo calls with interested schools

**Email Template**:
```
Subject: Free Student Grade Calculator for [School Name]

Hi [Principal Name],

I noticed [School Name] is known for academic excellence.

I've built a free grade & CGPA calculator that helps thousands
of students track their performance in real-time.

✓ Free for your students
✓ No installation needed
✓ Mobile-friendly
✓ Improves your website UX
✓ Helps with student retention

Would [School Name] be interested in using this? I can have
it embedded on your website within 24 hours.

Can we chat this Tuesday?

Best,
[Your Name]
[Phone]
```

**Daily Targets**:
- Day 32: Send 125 emails, collect 10-15 responses
- Day 33: Send 125 emails, collect 10-15 responses, schedule 5 calls
- Day 34: Send 125 emails, schedule 10 calls
- Day 35: Send 125 emails, close 10-15 partnerships

**Deliverable**: 10-15 school partnerships, 5-8 active embeds

---

### **DAY 36-38: Partnerships - Financial Advisors (3 days)**

#### Target: 20 Financial Partnerships by Day 38

**Outreach Strategy**:
- [ ] **Growth Lead**: Create list of 200 financial advisors / loan agents
- [ ] **Growth Lead**: Create partnership proposal (Google Doc)
- [ ] **Sales Rep**: Personalized outreach to 200 advisors
- [ ] **Growth Lead**: Track conversions

**Partnership Proposal**:
```markdown
## Calcarena + [Advisor Name] Partnership

### What We Offer:
- White-label EMI/loan calculator
- Embed on your website
- Zero commission upfront
- Your branding maintained

### What We Ask:
- When customer calculates EMI, show your loan offer
- Small "powered by Calcarena" link

### Revenue:
- 15% commission on referred loans

### Example:
Customer calculates EMI → Shows results → "Get personalized loan quote"
→ Click → Leads to your loan form → Conversion → 15% commission

### Next Steps:
- 30-min intro call
- Review calculator
- Design custom integration
- Go live in 1 week
```

**Daily Targets**:
- Day 36: Send 67 emails, schedule 5 calls
- Day 37: Send 67 emails, schedule 10 calls, close 3-5 partnerships
- Day 38: Send 66 emails, close 10-15 partnerships

**Deliverable**: 10-15 financial partnerships, embed live

---

### **DAY 39-40: Partnerships - Education Platforms (2 days)**

#### Target: 5-10 Education Platform Partnerships by Day 40

**Partners to Target**:
- Unacademy (JEE/NEET courses)
- Vedantu (Online tutoring)
- Testbook (Exam prep)
- Khan Academy
- Byjus

**Approach**:
- [ ] **Growth Lead**: Research partnership pages
- [ ] **Growth Lead**: Create partnership deck (2 pages)
- [ ] **Growth Lead**: Email partnership managers
- [ ] **Growth Lead**: Schedule calls

**Deck Outline**:
```
1. Problem: 50M students use calculators annually
2. Solution: Calcarena + your platform
3. Integration: JEE rank predictor → Unacademy courses
4. Metrics: 2K+ impressions/month per partnership
5. Revenue: 5-10% per lead conversion
6. CTA: Schedule 15-min call
```

**Daily Targets**:
- Day 39: Create deck, send to 10 platform managers, schedule 2 calls
- Day 40: Follow up, schedule 5 calls, close 2-3 partnerships

**Deliverable**: 2-5 education platform partnerships

---

### **DAY 41-42: Influencer Outreach (2 days)**

#### Target: 3-5 Influencer Collaborations

**Tier 3 Influencers** (100K-1M followers):
- Math & education channels
- Finance & investment channels
- Student communities

**Outreach**:
- [ ] **Marketing Lead**: Find 50 relevant influencers
- [ ] **Marketing Lead**: Create collab proposal
- [ ] **Marketing Lead**: Email with free usage offer

**Proposal Template**:
```
Subject: Free Calculator Tool for Your Audience

Hi [Influencer Name],

I love your content about [topic]. I've built a [keyword] calculator
that helps [audience] [solve problem].

Would you be interested in:
- Testing it free (no cost)
- Featuring it in a short video
- Earning commission on referrals (10%)

If interested, happy to hop on a quick call.

Best,
[Your Name]
```

**Daily Targets**:
- Day 41: Send 25 proposals, get 5-10 responses
- Day 42: Schedule 3-5 collab calls, close 2-3 collaborations

**Deliverable**: 2-3 influencer partnerships committed

**END OF PHASE 4**:
- ✅ Production live
- ✅ 30+ partnerships in pipeline
- ✅ 10-15 partnerships live with embeds
- ✅ 2-5K referral traffic/day coming in
- ✅ Influencer collaborations scheduled

---

## 📱 PHASE 5: SOCIAL & DISTRIBUTION (Days 43-56)

### **DAY 43-44: YouTube Shorts Strategy & Creation**

#### Day 43 (Planning & Recording):
- [ ] **Video Producer**: Create 20 short video ideas
- [ ] **Video Producer**: Record first 20 YouTube Shorts (30-60s each)
- [ ] **Video Producer**: Edit and add captions
- [ ] **Copywriter**: Write hooks & CTAs

**YouTube Shorts Ideas** (20-30s each):

| # | Idea | Hook | Duration | Est. Views |
|---|---|---|---|---|
| 1 | Age Calculator Hack | "Calculate your exact age in 3 seconds" | 20s | 100K |
| 2 | Percentage Trick | "The trick teachers don't want you to know" | 25s | 80K |
| 3 | EMI Surprise | "This calculator shocked me..." | 30s | 50K |
| 4 | CGPA Reality | "Is my CGPA good? Let's find out..." | 30s | 70K |
| 5 | Discount Secret | "Save 20% with this ONE trick" | 20s | 60K |
| 6 | Salary Truth | "What am I actually taking home?" | 30s | 90K |
| 7 | JEE Rank | "What rank will I get in JEE?" | 30s | 120K |
| 8 | BMI Check | "Am I overweight? Let's check..." | 25s | 100K |
| 9 | Conversion Trick | "100 CM in feet? Instantly..." | 20s | 80K |
| 10 | Compound Interest | "This is how you become rich 💰" | 30s | 110K |

#### Day 44 (Upload & Schedule):
- [ ] **Social Manager**: Upload 10 Shorts to YouTube
- [ ] **Social Manager**: Upload 10 Shorts to Instagram Reels
- [ ] **Social Manager**: Upload 10 Shorts to TikTok (if applicable)
- [ ] **Copywriter**: Write engaging descriptions
- [ ] **Social Manager**: Add calls-to-action (link in bio)
- [ ] **Growth Lead**: Set up UTM tracking

**Upload Schedule**:
```
Upload times for maximum reach:
- YouTube: 9 AM, 2 PM, 7 PM (India time)
- Instagram: 7 AM, 1 PM, 6 PM
- TikTok: 10 AM, 3 PM, 8 PM
```

**Deliverable**: 30 videos uploaded, scheduled

---

### **DAY 45-48: Content Production - Weeks 2 & 3 (4 days)**

#### Day 45 (Recording):
- [ ] **Video Producer**: Record 20 more YouTube Shorts
- [ ] **Video Producer**: Record 5 longer YouTube videos (2-3 min)

#### Day 46 (Editing):
- [ ] **Editor**: Edit all videos
- [ ] **Editor**: Add captions & graphics
- [ ] **Copywriter**: Write descriptions

#### Day 47 (Upload):
- [ ] **Social Manager**: Upload all 25 videos

#### Day 48 (Optimization):
- [ ] **Growth Lead**: Monitor analytics
- [ ] **Growth Lead**: Identify top-performing videos
- [ ] **Growth Lead**: Create more content around top performers

**Metrics to Track**:
- Watch time
- Click-through rate (CTR) to calculator
- Comment sentiment
- Shares

**Target**: 500K+ total views by Day 48

**Deliverable**: 60 videos produced + uploaded

---

### **DAY 49-50: Influencer Collaborations Launch (2 days)**

#### Day 49:
- [ ] **Marketing Lead**: Coordinate with 3-5 influencers
- [ ] **Marketing Lead**: Provide calculator links
- [ ] **Marketing Lead**: Create co-branded graphics

#### Day 50:
- [ ] **Influencers**: Publish content (staggered throughout day)
- [ ] **Growth Lead**: Monitor traffic & engagement
- [ ] **Growth Lead**: Track conversions

**Expected Impact**:
- 5K-10K views per influencer post
- 500-1K referral traffic
- 10-20 premium signups

**Deliverable**: Influencer posts live, results tracked

---

### **DAY 51-52: Instagram Feed & Community Building (2 days)**

#### Day 51:
- [ ] **Content Creator**: Create 10 carousel posts
  - Before/After calculations
  - Tips & tricks
  - Educational infographics
  - Calculator showcases

- [ ] **Social Manager**: Design graphics (Canva)
- [ ] **Copywriter**: Write captions

#### Day 52:
- [ ] **Social Manager**: Post 10 carousel posts
- [ ] **Community Manager**: Respond to comments
- [ ] **Community Manager**: Join relevant communities (engagement)
- [ ] **Growth Lead**: Track follower growth

**Expected Growth**:
- Day 48: 5K followers
- Day 52: 12K followers

**Deliverable**: Instagram community engaged, 10 posts published

---

### **DAY 53-54: Email Newsletter Setup (2 days)**

#### Day 53:
- [ ] **Growth Lead**: Set up email service (Brevo/ConvertKit)
- [ ] **Growth Lead**: Create welcome email series (3 emails)
- [ ] **Copywriter**: Write email copy

**Email Series**:
```
Email 1 (Welcome):
Subject: "You're in! Free calculator access + tips"
- Welcome to Calcarena
- Top 5 calculator uses
- Exclusive subscriber tip

Email 2 (Day 2):
Subject: "Did you know? Most people calculate this wrong..."
- Feature one calculator
- Common mistake
- How to avoid it

Email 3 (Day 5):
Subject: "New calculator alert: Try this..."
- New calculator
- Use case
- Success story
```

#### Day 54:
- [ ] **Growth Lead**: Set up signup form on website
- [ ] **Growth Lead**: Create lead magnet (free PDF: "Top 10 Calculator Hacks")
- [ ] **Growth Lead**: Configure autoresponders
- [ ] **Growth Lead**: Test email delivery

**Target**: 500 email subscribers by Day 54

**Deliverable**: Email list + automation working

---

### **DAY 55-56: Analytics Review & Optimization (2 days)**

#### Day 55:
- [ ] **Analytics Lead**: Review all metrics
  - Organic traffic: 5K-10K daily
  - Social traffic: 2K-5K daily
  - Referral traffic: 3K-5K daily
  - Total: 10K-20K daily users
  - Email subscribers: 500+

- [ ] **Analytics Lead**: Identify top performers
- [ ] **Analytics Lead**: Find growth opportunities

#### Day 56:
- [ ] **Product Lead**: Optimize low-performing pages
- [ ] **SEO Lead**: Check search rankings
- [ ] **Growth Lead**: Plan next week's content
- [ ] **All**: Team review + retrospective

**Deliverable**: Data-driven optimization plan created

**END OF PHASE 5**:
- ✅ 60 social videos created & published
- ✅ 2-5 influencer collaborations live
- ✅ Instagram followers: 12K+
- ✅ YouTube Shorts views: 500K+
- ✅ Email subscribers: 500+
- ✅ Daily traffic: 10K-20K users

---

## 💰 PHASE 6: MONETIZATION & SCALE (Days 57-90)

### **DAY 57-58: Ad Network Setup**

#### Day 57 (Google AdSense):
- [ ] **Growth Lead**: Apply to Google AdSense
- [ ] **Tech Lead**: Add ad tags to all pages
- [ ] **Tech Lead**: Implement ad manager
- [ ] **Tech Lead**: Test ad delivery

#### Day 58 (Other Networks):
- [ ] **Growth Lead**: Apply to AdThrive (if eligible)
- [ ] **Growth Lead**: Apply to Mediavine (if eligible)
- [ ] **Tech Lead**: Set up header bidding

**Expected Revenue**:
- Week 1: $50-100 (low initial traffic)
- Week 2: $200-500
- Week 3: $500-1K
- By Day 90: $3K-5K/month

**Deliverable**: Ad networks configured, ads serving

---

### **DAY 59-60: Premium Tier Launch**

#### Day 59:
- [ ] **Product Lead**: Design premium features
  - Ad-free experience
  - Result history (unlimited)
  - Batch calculations
  - Export to Excel/PDF

- [ ] **Dev Lead**: Build premium paywall (Stripe)
- [ ] **Dev Lead**: Implement feature flags

#### Day 60:
- [ ] **Copywriter**: Write premium marketing copy
- [ ] **Growth Lead**: Create upgrade prompts
- [ ] **Tech Lead**: Test payment flow
- [ ] **Social Manager**: Create upgrade videos

**Pricing**: $4.99/month or $49/year (20% discount)

**Expected Conversion**: 5% of 10K daily users = 500 premium users/month

**Deliverable**: Premium tier live, paywall working

---

### **DAY 61-63: B2B School Licensing (3 days)**

#### Day 61:
- [ ] **Growth Lead**: Create pricing tiers
  - School Plan: $500/year (500 students)
  - Coaching Plan: $1,000/year (unlimited)
  - District Plan: $5,000/year (multiple schools)

- [ ] **Copywriter**: Write B2B sales page
- [ ] **Product Lead**: Design school dashboard

#### Day 62:
- [ ] **Sales Lead**: Outreach to 100 schools from partnership list
- [ ] **Sales Lead**: Schedule demos
- [ ] **Growth Lead**: Create demo video

#### Day 63:
- [ ] **Sales Lead**: Conduct demos
- [ ] **Sales Lead**: Close first 3-5 deals
- [ ] **Tech Lead**: Set up school instances

**Expected Revenue**: $2.5K from 5 schools × $500 avg

**Deliverable**: B2B program launched, first 5 deals closed

---

### **DAY 64-65: API Developer Program (2 days)**

#### Day 64:
- [ ] **Dev Lead**: Create API documentation
- [ ] **Dev Lead**: Set up API dashboard
- [ ] **Growth Lead**: Create pricing
  - Free tier: 100 calls/day
  - Starter: $10/month (1K calls/day)
  - Pro: $50/month (100K calls/day)

#### Day 65:
- [ ] **Growth Lead**: Market to developers
  - Reddit (/r/webdev, /r/india)
  - Product Hunt
  - Dev newsletters
  - GitHub

**Expected Users**: 20-30 API customers by Day 90

**Deliverable**: API program live, first customers acquired

---

### **DAY 66-70: Affiliate Program Launch (5 days)**

#### Day 66-67 (Setup):
- [ ] **Growth Lead**: Choose affiliate network (ShareASale or custom)
- [ ] **Growth Lead**: Create affiliate dashboard
- [ ] **Growth Lead**: Design affiliate assets
- [ ] **Copywriter**: Write affiliate marketing guide

#### Day 68-69 (Outreach):
- [ ] **Growth Lead**: Email 50 finance blogs
- [ ] **Growth Lead**: Email 30 education blogs
- [ ] **Growth Lead**: Email 20 loan agents

#### Day 70:
- [ ] **Growth Lead**: Onboard first 10 affiliates
- [ ] **Growth Lead**: Monitor conversions
- [ ] **Growth Lead**: Send commission payouts

**Commission Structure**:
- 15% for loan referrals
- 10% for education platform signups
- 20% for B2B school licenses

**Expected Revenue**: $1-2K from 200+ referrals

**Deliverable**: Affiliate program live, first commissions paid

---

### **DAY 71-75: Content Expansion (5 days)**

#### Publish 20 More Blog Posts

**Daily Targets**:
- Day 71: Publish 5 blogs (write in advance, Day 26-28)
- Day 72: Publish 4 blogs
- Day 73: Publish 4 blogs
- Day 74: Publish 4 blogs
- Day 75: Publish 3 blogs

**Blog Focus**:
- Trending topics (IPL, salary, tax)
- High-volume seasonal keywords
- Niche areas with low KD

**Expected Impact**: 50 published blogs total = 10K-15K additional monthly traffic

**Deliverable**: 50 published blog posts

---

### **DAY 76-78: Chrome Extension Launch (3 days)**

#### Day 76 (Development):
- [ ] **Dev Lead**: Build Chrome extension
  - Features: Quick calculator access, unit converter
  - Context menu integration
  - Keyboard shortcut

#### Day 77 (Testing & Publishing):
- [ ] **QA Lead**: Test on Windows & Mac
- [ ] **Dev Lead**: Submit to Chrome Web Store
- [ ] **Growth Lead**: Prepare launch marketing

#### Day 78 (Launch):
- [ ] **Growth Lead**: Post on Product Hunt
- [ ] **Growth Lead**: Post on Reddit
- [ ] **Growth Lead**: Email list & social

**Expected Downloads**: 5K-10K in Week 1

**Deliverable**: Chrome extension published, marketing live

---

### **DAY 79-82: Regional Language Expansion (4 days)**

#### Day 79 (Hindi):
- [ ] **Content Lead**: Translate 30 popular calculators to Hindi
- [ ] **Content Lead**: Write 5 Hindi blog posts
- [ ] **Tech Lead**: Deploy Hindi URLs (/hi/emi-calculator/)

#### Day 80 (Tamil):
- [ ] **Content Lead**: Translate 20 calculators to Tamil
- [ ] **Content Lead**: Write 3 Tamil blog posts

#### Day 81 (Bengali):
- [ ] **Content Lead**: Translate 20 calculators to Bengali
- [ ] **Content Lead**: Write 3 Bengali blog posts

#### Day 82 (Optimization):
- [ ] **SEO Lead**: Optimize regional language pages
- [ ] **SEO Lead**: Submit to Google Search Console

**Expected Impact**: 5K-10K additional regional traffic

**Deliverable**: 3 languages live, 100+ translated pages

---

### **DAY 83-86: Performance & Growth Hacks (4 days)**

#### Day 83 (Referral Program):
- [ ] **Growth Lead**: Build referral system
- [ ] **Growth Lead**: Offer rewards (free premium month for 3 referrals)
- [ ] **Growth Lead**: Promote referral program

#### Day 84 (SEO Audit):
- [ ] **SEO Lead**: Run comprehensive SEO audit
- [ ] **SEO Lead**: Fix any critical issues
- [ ] **SEO Lead**: Identify quick wins

#### Day 85 (Conversion Optimization):
- [ ] **Product Lead**: A/B test calculator layouts
- [ ] **Product Lead**: A/B test CTA buttons
- [ ] **Product Lead**: Analyze user behavior (heatmaps)

#### Day 86 (Growth Metrics):
- [ ] **Analytics Lead**: Analyze all KPIs
- [ ] **Analytics Lead**: Identify top-performing channels
- [ ] **Growth Lead**: Plan doubling strategy

**Expected Metrics by Day 86**:
- Monthly users: 300K-500K
- Daily users: 15K-25K
- Monthly revenue: $30-50K
- Email subscribers: 3K+
- Social followers: 100K+ combined

**Deliverable**: Performance optimizations complete

---

### **DAY 87-90: Final Push & Q1 Planning (4 days)**

#### Day 87 (Viral Content):
- [ ] **Video Lead**: Create 5 viral video ideas
- [ ] **Video Lead**: Record & publish
- [ ] **Growth Lead**: Cross-promote on all channels

#### Day 88 (Analytics & Reporting):
- [ ] **Analytics Lead**: Generate 90-day report
- [ ] **Analytics Lead**: Create dashboard
- [ ] **Analytics Lead**: Present findings to team

#### Day 89 (Team Retrospective):
- [ ] **All**: 2-hour retrospective meeting
  - What worked
  - What didn't
  - Learnings
  - Q2 priorities

#### Day 90 (Celebration & Planning):
- [ ] **All**: Celebrate wins (team lunch/happy hour)
- [ ] **Leadership**: Plan Q2 roadmap
- [ ] **All**: Set new 90-day targets

**Final 90-Day Metrics**:
| Metric | Target | Actual |
|--------|--------|--------|
| Daily Users | 15K-25K | ? |
| Monthly Traffic | 500K+ | ? |
| Blog Posts | 50+ | ? |
| Calculators | 200+ | ? |
| Revenue | $50K/month | ? |
| Email Subscribers | 5K+ | ? |
| Social Followers | 100K+ | ? |

**Deliverable**: 90-day execution complete, Q2 roadmap ready

---

## 📊 DAILY STANDUP TEMPLATE

**Time**: 9 AM (15 minutes max)

**Each person answers**:
1. What did I complete yesterday?
2. What am I working on today?
3. Any blockers?

**Template**:
```
[Name]:
✅ Completed: [2-3 items]
🔄 Today: [2-3 tasks]
🚨 Blocker: [if any]

[Growth Lead]:
✅ Sent 25 partnership emails, got 3 responses
🔄 Following up with 10 schools, creating affiliate dashboard
🚨 None
```

---

## 🎯 SUCCESS CHECKLIST

### Phase 1 Success (Day 7):
- ✅ Repository set up
- ✅ Database configured
- ✅ Tech stack deployed
- ✅ Staging environment live

### Phase 2 Success (Day 21):
- ✅ 100 calculators built
- ✅ All pages have schema markup
- ✅ Mobile responsive & fast
- ✅ SEO basics in place

### Phase 3 Success (Day 28):
- ✅ 30 blog posts published
- ✅ Blog infrastructure complete
- ✅ Internal linking done
- ✅ All pages optimized

### Phase 4 Success (Day 42):
- ✅ Production live
- ✅ 10-15 partnerships signed
- ✅ Beta testing complete
- ✅ Influencer collaborations set

### Phase 5 Success (Day 56):
- ✅ 60 social videos published
- ✅ 2-5 influencer collabs live
- ✅ Daily traffic: 10K-20K users
- ✅ Email list: 500+

### Phase 6 Success (Day 90):
- ✅ Ad revenue generating
- ✅ Premium tier launched
- ✅ B2B deals closed
- ✅ API live
- ✅ Monthly revenue: $50K+

---

## 💰 BUDGET BREAKDOWN (90 Days)

| Item | Cost | Notes |
|------|------|-------|
| **Hosting & Infrastructure** | $500 | Vercel + Supabase |
| **Domain & SSL** | $50 | Annual |
| **Design & UI/UX** | $2,000 | Designer contractor |
| **Content Writing** | $3,000 | 3 writers × $1K each |
| **Video Production** | $2,000 | Shorts + longer videos |
| **Tools & Software** | $500 | SEO tools, analytics |
| **Paid Ads (testing)** | $2,000 | Google/Facebook ads |
| **Influencer Collabs** | $1,500 | 3 influencers × $500 |
| **Miscellaneous** | $500 | Unexpected costs |
| **TOTAL** | **$12,050** | ~$12K investment |

**Expected ROI**:
- Month 1: $2.5K revenue
- Month 2: $15.5K revenue
- Month 3: $45.5K revenue
- **Total 90-day revenue**: $63.5K
- **ROI**: 5.3x investment in 90 days

---

## 🔄 WEEKLY CHECK-IN TEMPLATE

**Every Friday, 4 PM**

**15-minute meeting, 6 people**

```
WEEK [X] REVIEW:

Traffic:
- Organic: [X] users/day (target: [Y])
- Social: [X] users/day (target: [Y])
- Referral: [X] users/day (target: [Y])
- Total: [X] users/day (target: [Y])

Content:
- Blogs published: [X] (target: [Y])
- Calculators built: [X] (target: [Y])
- Videos published: [X] (target: [Y])

Partnerships:
- New partnerships: [X] (target: [Y])
- Total partnerships: [X] (target: [Y])

Revenue:
- Ad revenue: $[X] (target: $[Y])
- Premium signups: [X] (target: [Y])
- Affiliate revenue: $[X] (target: $[Y])

Wins: [2-3 things that went well]
Challenges: [1-2 things to improve]
Next week focus: [Top 3 priorities]
```

---

## 🎬 END OF ACTION DOCUMENT

This document is your daily execution guide. Print it, post it, and follow it religiously.

**Success = Consistent execution of these tasks.**

Go build something amazing! 🚀

