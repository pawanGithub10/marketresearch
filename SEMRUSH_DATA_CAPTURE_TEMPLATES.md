# 📊 SEMRUSH DATA CAPTURE TEMPLATES
**Actionable Data Formats for Priority Dev & Enhancement Decisions**

---

## 🎯 TEMPLATE 1: CALCULATOR PRIORITY MATRIX
**Use this to decide which calculators to build first**

```csv
Calculator,India Volume,USA Volume,Global Volume,KD %,CPC,Intent,Featured Snippet,Days to Rank,Priority Score,Phase,Status
EMI Calculator,110000,85000,195000,15,2.50,Commercial,No,14,950,Phase 2,BUILD_WEEK_1
Percentage Calculator,90000,75000,165000,10,1.20,Transactional,No,7,920,Phase 2,BUILD_WEEK_1
Age Calculator,80000,65000,145000,12,0.80,Transactional,No,10,880,Phase 2,BUILD_WEEK_1
Temperature Converter,98000,72000,170000,12,0.50,Transactional,No,5,850,Phase 2,BUILD_WEEK_1
JEE Rank Predictor,45000,0,45000,35,0.00,Informational,No,21,750,Phase 2,BUILD_WEEK_2
CGPA Calculator,75000,42000,117000,12,0.30,Transactional,No,8,820,Phase 2,BUILD_WEEK_1
```

**Scoring Formula:**
```
Priority Score =
  (India Volume * 0.5) +           # 50% weight to India market
  (USA Volume * 0.2) +             # 20% weight to USA
  (Global Volume * 0.1) +          # 10% weight to other
  (CPC * 100 * 0.1) +              # 10% weight to revenue
  (100 - KD * 0.1)                 # Deduct for difficulty
```

**How to use:**
- Sort by Priority Score (highest first)
- Build calculators in this order
- High score = build Week 1-2
- Medium score = build Week 3-4
- Low score = build Week 5+ or deprioritize

---

## 🎯 TEMPLATE 2: KEYWORD OPPORTUNITY SPREADSHEET
**For blog writing and content strategy**

```csv
Blog Keyword,Search Volume,KD,Blog URL,Target Rank Position,Content Length,Sections Needed,Days to Write,Days to Rank,Calculator to Embed,Priority,Status
How to Calculate EMI,35000,18,/blog/how-to-calculate-emi,3,2000,5,2,21,EMI Calculator,High,WRITE_WEEK_1
How to Calculate Age,28000,10,/blog/how-to-calculate-age,2,1800,4,2,14,Age Calculator,High,WRITE_WEEK_1
How to Calculate Percentage,32000,12,/blog/how-to-calculate-percentage,2,2000,5,2,17,Percentage Calculator,High,WRITE_WEEK_1
How to Calculate CGPA,22000,14,/blog/how-to-calculate-cgpa,3,2200,6,2,19,CGPA Calculator,High,WRITE_WEEK_1
How to Calculate Income Tax India,42000,20,/blog/how-to-calculate-income-tax,5,2500,7,3,28,Income Tax Calculator,Medium,WRITE_WEEK_2
```

**How to use:**
- Sort by Priority (High first)
- Assign writers based on Days to Write
- Track progress in Status column
- Update Rank Position monthly
- When you hit top 3 → move to next blog

---

## 🎯 TEMPLATE 3: COMPETITOR BENCHMARK DATA
**For setting realistic goals and understanding market**

```csv
Competitor,Domain,Organic Traffic/Month,Total Calculators,Top Page Traffic,Avg Traffic/Page,Est Monthly Revenue,Your Target/Month,Timeline to Target
OmniCalculator,omnicaculator.com,25000000,600,45000,41667,750000,5000000,18 months
Calculator.net,calculator.net,15000000,200,32000,75000,450000,2500000,12 months
BYJU's Tools,tools.byjus.com,8000000,100,28000,80000,240000,1500000,10 months
RapidTables,rapidtables.com,12000000,150,22000,80000,360000,2000000,12 months
Calcarena.com (You),calcarena.com,0,100,0,0,0,500000,3 months
```

**How to use:**
- Monthly check-in (download fresh competitor data)
- Update your actual traffic/revenue
- Adjust 3-month, 6-month, 12-month targets
- Competitive benchmarking (are you on track?)
- Identify when you'll overtake each competitor

---

## 🎯 TEMPLATE 4: BACKLINK SOURCE OPPORTUNITIES
**For partnership and outreach priority**

```csv
Website,Domain Authority,Traffic,Calculator Category,Link Type,Anchor Text Pattern,Contact Status,Email,Pitch Date,Follow-up Date,Status
mathworld.wolfram.com,82,450000,Math,Editorial,math calculator,Researched,contact@wolfram.com,Pending,Pending,TODO
khanacademy.org,93,5000000,Education,Partnership,education calculator,Researched,partnerships@khanacademy.org,Pending,Pending,TODO
investopedia.com,92,3200000,Finance,Guest Post,financial calculator,Researched,editorial@investopedia.com,Pending,Pending,TODO
thoughtco.com,81,2100000,Education,Guest Post,educational tool,Researched,editorathoughtco@gmail.com,Pending,Pending,TODO
educationworld.com,75,890000,Education,Partnership,student tools,Researched,sales@educationworld.com,Pending,Pending,TODO
bankingupdate.in,48,450000,Finance India,Partnership,EMI calculator,Researched,contact@bankingupdate.in,Pending,Pending,TODO
```

**How to use:**
- Export from Semrush backlink analysis
- Filter by DA 30+ only
- Categorize by type (Editorial, Partnership, Affiliate)
- Create outreach priority list
- Track all communications
- Phase 4 (Days 29-42): Execute this list

---

## 🎯 TEMPLATE 5: SEASONAL PROMOTION CALENDAR
**For timing launches and marketing campaigns**

```csv
Calculator,Category,Peak Month(s),Peak Volume,Off-Season Volume,Peak:Off Ratio,Launch Date,Marketing Budget Allocation,Blog Post Date,Social Campaign Start,Expected Peak Traffic
Income Tax Calculator,Finance,Feb-March,250000,35000,7.1x,2024-01-15,30%,2024-01-01,2024-01-20,250000
JEE Rank Predictor,Exam,Apr-June,180000,12000,15x,2024-03-01,25%,2024-02-15,2024-03-20,180000
NEET Score Calculator,Exam,May-July,165000,10000,16.5x,2024-04-01,25%,2024-03-15,2024-04-20,165000
BMI / Fitness,Health,Jan-Feb,120000,45000,2.7x,2024-12-15,15%,2024-12-01,2024-12-20,120000
Pregnancy Calculator,Health,Steady,65000,60000,1.1x,2024-01-01,5%,2023-12-15,2024-01-15,70000
IPL Auction Calculator,Sports,Mar-April,100000,5000,20x,2024-02-15,20%,2024-02-01,2024-02-20,100000
```

**How to use:**
- Plan launch schedule (build high-peak first)
- Allocate marketing budget to peak months
- Publish blogs 4 weeks before peak
- Launch social campaigns 2 weeks before peak
- Track actual vs projected traffic

---

## 🎯 TEMPLATE 6: CONTENT STRUCTURE ANALYSIS
**For writing winning calculator descriptions & blogs**

```csv
Calculator,Winning Content Length,H2 Count,H3 Count,Images Count,Internal Links,External Links,FAQ Questions,Has Table,Has Formula,Has Examples,Bounce Rate,Avg Time on Page
EMI Calculator,2200,6,12,3,5,2,6,Yes,Yes,Yes,38%,4:12 min
Percentage Calculator,1800,5,10,2,4,1,5,Yes,Yes,Yes,35%,3:45 min
Temperature Converter,1200,4,8,2,3,1,4,Yes,No,Yes,42%,2:50 min
Grade Calculator,2000,5,11,3,4,2,5,Yes,Yes,Yes,40%,3:58 min
Age Calculator,1600,4,9,2,4,1,4,Yes,Yes,Yes,36%,3:22 min
```

**How to use:**
- Use as template for your content
- Target word count = what's winning
- Include recommended H2/H3 count
- Add tables, formulas, examples (proven winners)
- Monitor bounce rate vs industry
- If >45% bounce rate = content not satisfying

---

## 🎯 TEMPLATE 7: FEATURED SNIPPET OPPORTUNITIES
**For quick wins in search rankings**

```csv
Keyword,Current Rank Position,Has Snippet,Snippet Type,Snippet Owner,Can You Win,Content Strategy,Days to Implement,Expected Traffic Gain,Priority
How to calculate EMI,5,Yes,Table,OmniCalculator,Yes,Better table + step-by-step,3,+15%,High
Percentage calculator formula,8,No,None,N/A,Yes,Add formula section + examples,2,+20%,High
Temperature converter,3,No,None,N/A,Yes,Simple conversion table,1,+25%,High
Age calculation formula,12,No,None,N/A,Yes,Formula + worked example,2,+18%,High
CGPA calculation method,7,Yes,List,Wikipedia,Maybe,Better list format,3,+10%,Medium
```

**How to use:**
- Target "No snippet" keywords first (easier win)
- Add featured snippet format to content
- Expected 15-30% traffic increase
- Quick content additions (2-3 days)
- High ROI improvement

---

## 🎯 TEMPLATE 8: INDIA VS INTERNATIONAL SPLIT
**For regional strategy and language prioritization**

```csv
Calculator,India Volume,USA Volume,UK Volume,Canada Volume,India %,Language Priority 1,Language Priority 2,India-Specific Version,Monetization Focus
EMI Calculator,110000,85000,22000,12000,52%,English,Hindi,Yes,Affiliate + Ads
Income Tax Calculator,95000,32000,8000,4000,67%,Hindi,English,Yes,Ads + Premium
JEE Rank Predictor,45000,0,0,0,100%,Hindi,English,Yes,Premium
BMI Calculator,58000,72000,18000,15000,35%,English,Hindi,No,Ads + Premium
Salary Calculator,72000,45000,12000,8000,48%,Hindi,English,Yes,Affiliate + Ads
NEET Score,38000,0,0,0,100%,English,Hindi,Yes,Premium
Percentage Calculator,90000,75000,20000,15000,45%,English,Hindi,No,Ads
```

**How to use:**
- India >60% = Build Hindi version ASAP
- India >50% = Make Hindi version priority
- India <40% = Delay Hindi translation
- 100% India = Optimize for Hindi speakers
- High India % = Focus on India partnerships

**Action items:**
- Week 3: Build Hindi versions for high-India-% calculators
- Week 4: Optimize for Hindi search intent
- Week 5: Add Hindi metadata & SEO

---

## 🎯 TEMPLATE 9: MONETIZATION REVENUE POTENTIAL
**For calculating expected monthly revenue per calculator**

```csv
Calculator,Monthly Organic Traffic,Avg Pages/Visit,Ad Impressions,CPM Rate,Ad Revenue,Premium Conversion,Premium Revenue,Affiliate Potential,Total Est Revenue,Rank by Revenue
EMI Calculator,15000,1.8,27000,2.5,67.50,3%,450,10%,15000,#1
Income Tax,12000,1.8,21600,3.0,64.80,5%,450,8%,12000,#3
Loan Calculator,10000,1.8,18000,2.8,50.40,2%,200,15%,18000,#2
CGPA Calculator,8000,1.8,14400,1.0,14.40,8%,800,1%,9000,#5
BMI Calculator,7500,1.8,13500,1.2,16.20,2%,100,0.5%,2000,#8
Salary Calculator,6000,1.8,10800,2.0,21.60,4%,300,12%,8500,#6
```

**How to use:**
- Calculate expected revenue per calculator
- High revenue calculators = build first
- Low revenue = deprioritize or enhance
- Track actual vs projected
- Adjust CPM/conversion assumptions monthly

**Formula:**
```
Ad Revenue = (Traffic * Pages/Visit) * (CPM / 1000)
Premium Revenue = Traffic * Premium Conversion Rate * Price
Affiliate Revenue = Traffic * Affiliate Click Rate * Commission
Total = Ad Revenue + Premium Revenue + Affiliate Revenue
```

---

## 🎯 TEMPLATE 10: PHASE-WISE BUILD PRIORITY
**Exact sequence for what to build when**

### PHASE 2: DAYS 8-21 (Build 100 Calculators)

**Week 1 (Days 8-9): TOP 10 HIGH-VOLUME, LOW-KD**
```
1. EMI Calculator (110K vol, 15% KD) → Est 5K traffic/month
2. Percentage Calculator (90K vol, 10% KD) → Est 4K traffic/month
3. Age Calculator (80K vol, 12% KD) → Est 3.5K traffic/month
4. Temperature Converter (98K vol, 12% KD) → Est 4.2K traffic/month
5. CM to Inches (120K vol, 8% KD) → Est 5.5K traffic/month
6. KG to LBS (110K vol, 10% KD) → Est 4.8K traffic/month
7. Loan Calculator (85K vol, 16% KD) → Est 3.2K traffic/month
8. Grade Calculator (60K vol, 12% KD) → Est 2.5K traffic/month
9. BMI Calculator (95K vol, 14% KD) → Est 3.8K traffic/month
10. CGPA Calculator (75K vol, 12% KD) → Est 3K traffic/month

TOTAL WEEK 1 TARGET: ~40K monthly traffic
```

**Week 2 (Days 10-14): NEXT 30 (High Volume + Strategic)**
```
Group 1 - Finance (5 calculators):
- Simple Interest (45K vol)
- Compound Interest (60K vol)
- SIP Calculator (75K vol)
- Discount Calculator (40K vol)
- ROI Calculator (38K vol)

Group 2 - Converters (10 calculators):
- Miles to Kilometers (80K vol)
- Liters to Gallons (82K vol)
- Grams to Ounces (88K vol)
- Meters to Feet (95K vol)
- Pounds to Kilograms (105K vol)
... (5 more)

Group 3 - Education (8 calculators):
- SGPA Calculator (42K vol)
- GPA Calculator (65K vol)
- Percentage from Marks (90K vol)
- Weighted Average (14K vol)
... (4 more)

Group 4 - Time/Date (7 calculators):
- Date Difference (35K vol)
- Days Calculator (25K vol)
... (5 more)

TOTAL WEEK 2 TARGET: ~50K monthly traffic
```

**Week 3 (Days 15-18): BATCH 3 - REMAINING 60**
- Follow same ranking by volume/KD
- Process 15 calculators/day
- Total target: ~30K monthly traffic

---

## 🎯 TEMPLATE 11: QUALITY CONTROL CHECKLIST
**Before publishing each calculator**

```csv
Calculator,Schema Markup,Mobile Optimized,Meta Tags,Related Links,FAQ Added,Formula Explained,Share Button,Save Feature,Example Added,Status
EMI Calculator,✓,✓,✓,✓,✓,✓,✓,✓,✓,LIVE
Age Calculator,✓,✓,✓,✓,✓,✓,✓,✓,✓,LIVE
Percentage,✓,✓,✓,⚠,✓,✓,✓,✓,✓,QA
Temperature,✓,✓,✓,✓,✗,✓,✓,✓,✓,IN_PROGRESS
```

**How to use:**
- Create before-launch checklist
- Don't publish until all ✓
- ⚠ = needs attention
- ✗ = fix before publish
- Track completion %

---

## 🎯 TEMPLATE 12: MONTHLY TRACKING & ADJUSTMENT
**For ongoing optimization**

```csv
Metric,Week 1,Week 2,Week 3,Week 4,Target,Variance,Action Needed
Calculators Live,10,30,70,100,100,0%,On track
Blog Posts,3,10,25,35,50,-30%,Speed up writing
Organic Traffic/Day,500,2000,5000,8000,10000,-20%,Needs SEO boost
Social Followers,2000,8000,25000,50000,50000,0%,On track
Email Subscribers,50,300,800,1500,2000,-25%,Improve lead magnet
Partnerships,2,8,15,25,30,-17%,More outreach
Ad Revenue,$0,$50,$400,$1200,$2000,-40%,Needs more traffic
Affiliate Leads,0,5,35,120,200,-40%,More partnerships needed
```

**How to use:**
- Update weekly
- Compare to target
- Variance >-20% = action needed
- Identify bottlenecks early
- Adjust Phase 2-6 accordingly

---

## 📥 DATA EXPORT WORKFLOW

### Step 1: Organize Semrush Downloads
```
Create folder structure:
/semrush_data/
  ├── /keywords/
  │   ├── target_keywords_india.csv
  │   ├── target_keywords_usa.csv
  │   ├── long_tail_keywords.csv
  │   └── question_keywords.csv
  │
  ├── /competitors/
  │   ├── omnicaculator_domain_overview.csv
  │   ├── omnicaculator_top_pages.csv
  │   ├── calculator_net_top_pages.csv
  │   └── competitor_backlinks_da30plus.csv
  │
  ├── /content_analysis/
  │   ├── serp_analysis_top30.csv
  │   ├── featured_snippets.csv
  │   └── content_structure.csv
  │
  ├── /india_data/
  │   ├── keywords_india_volume.csv
  │   ├── keywords_state_breakdown.csv
  │   └── language_preferences.csv
  │
  └── /trends/
      ├── seasonal_trends.csv
      └── monthly_volumes.csv
```

### Step 2: Convert to Master Spreadsheet
- Import all CSVs into one Google Sheet
- Create tabs for each template above
- Color-code priority levels (Red=High, Yellow=Med, Green=Low)
- Share with team

### Step 3: Create Actionable Outputs
- Template 1: Build calculator priority list
- Template 2: Blog writing assignment list
- Template 5: Launch calendar
- Template 10: Phase 2 exact build sequence

---

## 🚀 HOW TO IMMEDIATELY USE THIS DATA

**Day 1 of Execution:**
- Use Template 10 to assign Day 8-9 calculator builds
- Use Template 3 to set realistic revenue targets
- Use Template 5 to plan launch timing

**Week 1 of Phase 2:**
- Use Template 1 to prioritize calculator builds
- Use Template 11 as QA checklist
- Use Template 12 to track progress

**Week 2 of Phase 2:**
- Use Template 2 to assign blog writing
- Use Template 9 to calculate expected revenue
- Use Template 4 to start partnership outreach (Phase 4 prep)

**Weeks 3-4 of Phase 2:**
- Use Template 6 to optimize content structure
- Use Template 7 to go after featured snippets
- Use Template 8 to plan Hindi version strategy

---

## 📊 INTEGRATION WITH YOUR DOCUMENTS

**Update ACTION_DOCUMENT.md:**
- Replace generic "build calculators" with Template 10 (exact sequence)
- Add Template 1 as decision framework

**Update SPECIFIC_PLAN_DOCUMENT.md:**
- Add Template 6 as content structure guide
- Add Template 11 as development checklist

**Keep as Reference:**
- Template 3 for monthly competitor reviews
- Template 12 for weekly progress tracking

---

## ✅ FINAL CHECKLIST

- [ ] Downloaded all Semrush data (Priority 1-6)
- [ ] Organized data in folder structure
- [ ] Created master spreadsheet with all templates
- [ ] Filled in Template 1 (Calculator Priority Matrix)
- [ ] Filled in Template 10 (Phase 2 Build Sequence)
- [ ] Shared with team/stakeholders
- [ ] Ready to execute with data-driven decisions
- [ ] Will update Template 12 (Tracking) weekly

---

**Now execute Phase 2 with actual data, not guesses!** 🚀

