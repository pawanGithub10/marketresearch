# YouTube Automation Scripts: Quick Start Guide

## Overview

This guide shows you exactly how to use the Python scripts provided to automate your YouTube channel setup and optimization.

---

## Setup Instructions

### Step 1: Install Requirements

```bash
# Create project directory
mkdir youtube_automation
cd youtube_automation

# Create virtual environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install required packages
pip install requests
```

### Step 2: Create Script Files

Create the following Python files in your `youtube_automation` directory:

**File 1:** `niche_validator.py` - Copy entire NicheValidator script from Part 3
**File 2:** `content_calendar.py` - Copy entire ContentCalendarGenerator script from Part 3
**File 3:** `affiliate_manager.py` - Copy entire AffiliateManager script from Part 3
**File 4:** `analytics_dashboard.py` - Copy entire YouTubeAnalyticsDashboard script from Part 3

---

## Quick Start Workflow

### **PHASE 1: Niche Research (30 minutes)**

#### Step 1a: Validate Your Niches

```bash
cd youtube_automation
python3 niche_validator.py
```

**What this does:**
- Scores each niche 0-100
- Shows recommendation (Excellent/Good/Fair/Poor)
- Exports results to `niche_analysis_[timestamp].json`

**Example output:**
```
🟢 EXCELLENT - Launch immediately: AI Tools for Dentists (Score: 92/100)
  - Excellent search volume (50k+)
  - Low competition (KD < 30)
  - Excellent CPM ($15+)
  - Multiple monetization streams

🟢 GOOD - Proceed with confidence: Zapier for Shopify (Score: 85/100)
```

**Action:** Choose the top-scoring niche

---

### **PHASE 2: Content Planning (45 minutes)**

#### Step 2a: Generate Content Calendar

```bash
python3 content_calendar.py
```

**What this does:**
- Generates 30 video topics automatically
- Assigns to content pillars (How-To, Reviews, Guides, etc.)
- Calculates SEO score for each title
- Exports to `content_calendar_[niche]_[timestamp].json`

**Example output:**
```
📅 Content Calendar for 'AI Tools for Dentists'

#1 | 2025-11-24 Monday
Title: How to Use ChatGPT for Dentists: Step-by-Step
Pillar: How-To Tutorial | SEO Score: 78/100 | Status: Planning

#2 | 2025-11-26 Wednesday
Title: Best AI Tools for Dentists: Complete Comparison
Pillar: Reviews & Comparisons | SEO Score: 85/100 | Status: Planning
```

**Action:** Review calendar, modify topics if desired

---

### **PHASE 3: Monetization Setup (1 hour)**

#### Step 3a: Create Affiliate Program List

```bash
python3 affiliate_manager.py
```

**What this does:**
- Adds all affiliate programs for your niche
- Creates tracking links with UTM parameters
- Sets up earnings tracking
- Exports affiliate link list to CSV

**Example for "AI Tools for Dentists" niche:**

```
✅ Added program: Make.com Affiliate (30% commission)
✅ Added program: Zapier Affiliate (30% commission)
✅ Added program: Airtable Partner (25% commission)
✅ Added program: Amazon Associates (5-10% commission)

🔗 Created affiliate links:
   - Make.com Automation Setup: [tracking URL]
   - Zapier Workflow Templates: [tracking URL]
   - Airtable for Dentistry: [tracking URL]
```

**Action:** Copy affiliate links, save them in a spreadsheet

---

### **PHASE 4: Analytics Setup (20 minutes)**

#### Step 4a: Initialize Analytics Dashboard

```bash
# Add your first 2-3 videos after publishing
python3 analytics_dashboard.py
```

**What this does:**
- Tracks video performance metrics
- Shows top performing videos
- Generates optimization recommendations
- Exports report

**Example dashboard:**
```
📊 YOUTUBE CHANNEL ANALYTICS DASHBOARD

📈 Channel Metrics:
  total_videos: 5
  total_views: 12,500
  total_watch_hours: 4,200
  subscribers_gained: 42
  average_engagement_rate: 2.15%
  total_revenue: $42.50

🏆 Top 5 Videos:
  1. "5 AI Tools That Let You Charge 3X More"
     Views: 2,500 | Watch Hours: 1,200 | Performance Score: 87/100
```

---

## Full Automation Workflow (Repeating Weekly)

### **Monday: Niche & Content Strategy**

```bash
# Review previous week's performance
python3 analytics_dashboard.py

# Identify top topics from analytics
# Plan next week's 3 video topics
```

### **Tuesday-Wednesday: Content Planning**

```bash
# Use ChatGPT prompt from Implementation Guide:
# "Write a 4-5 minute YouTube script about: [topic]"

# Save scripts in: scripts/week_[number]/

# Example structure:
scripts/
├── week_1/
│   ├── video_1_script.txt
│   ├── video_2_script.txt
│   └── video_3_script.txt
```

### **Thursday: Video Production**

```bash
# Generate voiceovers with Eleven Labs
# Edit videos with DaVinci Resolve
# Create thumbnails with Canva

# Organization:
videos/
├── week_1/
│   ├── video_1_final.mp4
│   ├── video_1_thumbnail.png
│   └── video_1_description.txt
```

### **Friday: Publishing & Link Management**

```bash
# Publish videos to YouTube
# Update affiliate links in descriptions

# Log conversion for affiliate tracking
python3 << 'EOF'
from affiliate_manager import AffiliateManager

manager = AffiliateManager()
manager.add_program("Make.com", "https://make.com", 30)

# Log a conversion
link = manager.create_affiliate_link(
    program_id=1,
    product_name="Make.com Setup",
    product_url="https://make.com/signup",
    video_id="your_video_id"
)

# After getting conversions from analytics
manager.log_conversion(link['id'], clicks=150, conversions=3, revenue=90.0)
manager.generate_report()
EOF
```

### **Sunday: Analytics Review**

```bash
# Fetch YouTube Analytics
# Update dashboard
python3 analytics_dashboard.py

# Review recommendations and plan next week
```

---

## Advanced Usage: Custom Scripts

### Running All Automations Daily

**Create:** `run_daily_automation.sh`

```bash
#!/bin/bash
# Daily automation script

echo "🤖 Running Daily YouTube Automation..."
echo "================================"

# 1. Check analytics
echo "📊 Checking analytics..."
python3 youtube_automation/analytics_dashboard.py

# 2. Check affiliate performance
echo "💰 Checking affiliate performance..."
python3 << 'EOF'
from youtube_automation.affiliate_manager import AffiliateManager
manager = AffiliateManager()
# Your affiliate tracking code here
EOF

# 3. Generate optimization report
echo "⚙️ Generating optimization report..."
python3 youtube_automation/analytics_dashboard.py > reports/daily_report_$(date +%Y-%m-%d).txt

echo "✅ Daily automation complete!"
```

**Run it:**
```bash
chmod +x run_daily_automation.sh
./run_daily_automation.sh
```

---

## Customizing Scripts for Your Niche

### Example: Customizing for "Micro-Finance: Tax Strategies"

**Step 1:** Modify `niche_validator.py` to add your niches:

```python
test_niches = [
    "tax strategies for freelancers",
    "cryptocurrency tax optimization",
    "real estate deductions",
    "w-2 employee side income"
]

results = validator.analyze_multiple_niches(test_niches)
```

**Step 2:** Modify `content_calendar.py` for your specific niche:

```python
generator = ContentCalendarGenerator(
    niche="Tax Strategies for Freelancers",
    upload_frequency=3  # 3 videos per week
)

# Topics will be auto-generated for this niche
generator.print_calendar()
generator.export_calendar(format='json')
```

**Step 3:** Modify `affiliate_manager.py` for your programs:

```python
manager = AffiliateManager()

# Tax/Finance specific programs
manager.add_program("TurboTax Affiliate", "https://turbotax.com/partners", 25)
manager.add_program("FreshBooks", "https://freshbooks.com/affiliate", 30)
manager.add_program("E-Trade", "https://etrade.com/partners", 15)
manager.add_program("CoinTracker", "https://cointracker.io/affiliate", 20)
```

---

## Real Example: "AI Tools for Dentists"

### Complete Setup (Copy & Paste Ready)

```python
#!/usr/bin/env python3
"""
Complete setup for AI Tools for Dentists YouTube channel
Ready to run - just execute this script
"""

from niche_validator import NicheValidator
from content_calendar import ContentCalendarGenerator
from affiliate_manager import AffiliateManager
from analytics_dashboard import YouTubeAnalyticsDashboard

print("🚀 YouTube Channel Automation Setup")
print("=" * 60)

# STEP 1: Validate Niche
print("\n📊 STEP 1: Validating Niche...")
validator = NicheValidator()
results = validator.analyze_multiple_niches([
    "AI tools for dentists",
    "ChatGPT for dental practices",
    "AI automation for dentistry"
])

print(f"✅ Niche validation complete")

# STEP 2: Generate Content Calendar
print("\n📅 STEP 2: Generating Content Calendar...")
generator = ContentCalendarGenerator(
    niche="AI Tools for Dentists",
    upload_frequency=3
)
calendar = generator.generate_calendar()
generator.export_calendar(format='json')
print(f"✅ Generated {len(calendar)} video topics")

# STEP 3: Setup Affiliate Programs
print("\n💰 STEP 3: Setting up Affiliate Programs...")
manager = AffiliateManager()

# Dental practice software
manager.add_program(
    name="Make.com Affiliate",
    url="https://make.com/partners/affiliate",
    commission_rate=30,
    payment_model='cps'
)

manager.add_program(
    name="Zapier Affiliate",
    url="https://zapier.com/partners/affiliate-program",
    commission_rate=30,
    payment_model='cps'
)

manager.add_program(
    name="Airtable Partner",
    url="https://airtable.com/partners",
    commission_rate=25,
    payment_model='cps'
)

manager.add_program(
    name="Amazon Associates",
    url="https://amazon.com/associates",
    commission_rate=5,
    payment_model='cps'
)

print("✅ Affiliate programs configured")

# STEP 4: Create Affiliate Links
print("\n🔗 STEP 4: Creating Affiliate Links...")
affiliate_links = []

for video_num in range(1, 6):
    link = manager.create_affiliate_link(
        program_id=1,
        product_name=f"Video {video_num} - Make.com Setup",
        product_url="https://make.com/signup",
        video_id=f"video_{video_num:03d}"
    )
    affiliate_links.append(link)

# Export all links
manager.export_links(format='csv')
print("✅ Affiliate links created and exported")

# STEP 5: Initialize Analytics
print("\n📈 STEP 5: Initializing Analytics Dashboard...")
dashboard = YouTubeAnalyticsDashboard()
print("✅ Analytics dashboard initialized")

# Final Summary
print("\n" + "=" * 60)
print("🎉 SETUP COMPLETE!")
print("=" * 60)
print("\n✅ Your YouTube channel is ready to launch:")
print(f"   • Niche: AI Tools for Dentists")
print(f"   • Video topics: {len(calendar)}")
print(f"   • Affiliate programs: 4")
print(f"   • Affiliate links: Ready to use")
print(f"\n📂 Files created:")
print(f"   • niche_analysis_[timestamp].json")
print(f"   • content_calendar_AI_Tools_for_Dentists_[timestamp].json")
print(f"   • affiliate_links_[timestamp].csv")
print(f"\n🚀 Next steps:")
print(f"   1. Create YouTube channel")
print(f"   2. Write first 5 video scripts (use ChatGPT)")
print(f"   3. Generate voiceovers (Eleven Labs)")
print(f"   4. Edit videos (DaVinci Resolve)")
print(f"   5. Publish with affiliate links")
```

**Run it:**
```bash
python3 setup_ai_dentists_channel.py
```

---

## Monitoring & Reporting

### Weekly Report Generator

```python
#!/usr/bin/env python3
"""Generate weekly performance report"""

from datetime import datetime
from analytics_dashboard import YouTubeAnalyticsDashboard
from affiliate_manager import AffiliateManager

print(f"\n📊 WEEKLY REPORT - {datetime.now().strftime('%Y-%m-%d')}")
print("=" * 80)

# Load your channel data
dashboard = YouTubeAnalyticsDashboard()
# Add your actual video data here

metrics = dashboard.calculate_channel_metrics()
print("\n📈 Channel Performance:")
for key, value in metrics.items():
    print(f"   {key}: {value}")

# Affiliate performance
manager = AffiliateManager()
# Load your affiliate data here

print("\n💰 Top Affiliate Links:")
recommendations = dashboard.get_video_recommendations()
# Display top opportunities

print("\n💡 Optimization Priorities:")
for rec in recommendations:
    if rec['recommendations']:
        print(f"\n   📹 {rec['title']}")
        for r in rec['recommendations']:
            if r['priority'] == 'High':
                print(f"      🔴 {r['issue']}: {r['recommendation']}")
```

---

## Troubleshooting

### Issue: Script won't run

```bash
# Check Python version
python3 --version  # Should be 3.7+

# Verify virtual environment is activated
which python3  # Should show path to venv

# Reinstall requirements
pip install --upgrade pip
pip install requests
```

### Issue: Can't import modules

```bash
# Make sure you're in correct directory
pwd  # Should be youtube_automation/

# Check files exist
ls *.py  # Should list all script files

# Try running with full path
python3 /path/to/youtube_automation/niche_validator.py
```

---

## Next Steps

1. **Complete Setup:** Run the setup script for your chosen niche
2. **Create Channel:** Use your content calendar to plan content
3. **First Videos:** Use ChatGPT prompts + Eleven Labs + DaVinci Resolve
4. **Track Performance:** Use analytics dashboard weekly
5. **Optimize:** Use recommendations from scripts to improve
6. **Scale:** Once profitable, add more niches

---

## Files Generated

```
youtube_automation/
├── niche_validator.py
├── content_calendar.py
├── affiliate_manager.py
├── analytics_dashboard.py
├── setup_[your_niche].py
├── run_daily_automation.sh
│
├── outputs/
│   ├── niche_analysis_2025-11-24.json
│   ├── content_calendar_AI_Tools_for_Dentists_2025-11-24.json
│   ├── affiliate_links_2025-11-24.csv
│   └── reports/
│       └── daily_report_2025-11-24.txt
│
├── scripts/
│   ├── week_1/
│   │   ├── video_1_script.txt
│   │   ├── video_2_script.txt
│   │   └── video_3_script.txt
│
└── videos/
    ├── week_1/
    │   ├── video_1_final.mp4
    │   ├── video_1_thumbnail.png
    │   └── video_1_description.txt
```

---

## Summary

**You now have:**
- ✅ 4 production-ready Python scripts
- ✅ Complete automation workflow
- ✅ Real-world examples for your niche
- ✅ Analytics & tracking system
- ✅ Affiliate management tools
- ✅ Daily automation setup

**Time to revenue:** 6-12 months with consistent execution
**Estimated Year 1 income:** $10,000-60,000 depending on niche

**Start today. Run the scripts. Launch your channel.** 🚀
