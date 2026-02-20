# LISTING LAUNCH

**Realty ONE Group Authentic** | Agent Recruiting & Shared Services Program

> You sell. We launch.

---

## What Is This?

Listing Launch is a complete listing services program built for Realty ONE Group Authentic. It provides agents with a full back-office team that handles everything from photography scheduling to marketing to transaction coordination, so agents can focus on what they do best: selling.

This repository contains all source code for the program's marketing assets, agent-facing tools, operations infrastructure, and training materials.

---

## Brand Specs

| Element | Value |
|---|---|
| **Primary Gold** | `#C5A95E` (HSL: 43 40% 57%) |
| **Background** | `#000000` (pure black) |
| **Card Background** | `hsl(0, 0%, 10%)` |
| **Text Primary** | `#FFFFFF` |
| **Text Secondary** | `rgba(255,255,255,0.7)` |
| **Text Muted** | `#999999` |
| **Headline Font** | Bebas Neue (always uppercase) |
| **Body Font** | Open Sans (300, 400, 600, 700) |
| **Accent/Quote Font** | Raleway (italic) |
| **Subheading Font** | Montserrat (600-900) |
| **Border Radius** | Sharp corners on cards (edgy, not corporate) |
| **Vibe** | Premium streetwear, not corporate. Bold, raw, high-contrast. |

Full branding spec: [[ROG_Authentic_Branding_Guide.txt](./docs/ROG_Authentic_Branding_Guide.txt)](https://github.com/scottbtherealtor/listing-launch/blob/main/ROG_Authentic_Brand_Guidelines_v2)

---

## Repository Structure

```
listing-launch/
├── README.md
├── docs/
│   ├── ROG_Authentic_Branding_Guide.txt
│   ├── service-model.md
│   └── pricing.md
├── marketing/
│   ├── teaser-campaign/
│   │   ├── post-1-something-is-coming.html
│   │   ├── post-2-doing-all-of-it.html
│   │   ├── post-3-video-script.md
│   │   ├── post-4-85-percent.html
│   │   ├── post-5-video-script.md
│   │   ├── post-6-tomorrow.html
│   │   └── email-campaign.md
│   ├── recruiting/
│   │   ├── grinder-flyer.html
│   │   └── persona-framework.md
│   └── landing-page/
│       └── (coming soon)
├── portal/
│   ├── listing-launch-portal.html
│   └── listing-launch-portal.jsx
├── forms/
│   ├── opnform-prelisting-prompt-v3.md
│   └── opnform-buyer-tc-prompt.md
├── operations/
│   ├── master-tracker-v2.xlsx
│   ├── zapier-setup.md
│   └── va-reference.pdf
├── training/
│   ├── launch-plan-training-guide.html
│   ├── launch-plan-training.pdf
│   └── launch-plan-training.docx
└── assets/
    └── (logos, images, fonts)
```

---

## Program Overview

### Service Model

Agents who qualify (8+ transaction sides in prior 12 months) get access to the Listing Launch team. On every listing, the team handles:

| Service | Description |
|---|---|
| **Full Listing TC** | Contract to close transaction coordination |
| **Photography** | Scheduling professional photography (4-5:30pm window) |
| **Pre-Listing Cleaning** | Scheduled morning of photo day |
| **Listing Home Warranty** | Enrolled automatically on listing date |
| **Open House Materials** | Prepared and delivered |
| **Just Listed Social Posts** | Created and posted |
| **Listing Blast Email** | Sent to agent network |
| **Property Website** | Built and promoted |
| **Just Sold Social Posts** | Posted after closing |

Buyer-side TC is also available as a separate submission.

### Pricing (Under Consideration)

Two models being evaluated. Both include $150/month base + $1,225/transaction fee.

**Option A: 10% Commission Split**

| Component | Amount |
|---|---|
| Monthly fee | $150 |
| Per-transaction fee | $1,225 |
| Commission split | 10% |
| Annual commitment | Required |

Agent nets 72.4% on 10 sides / $80K gross ($57,950).
Brokerage profit at 5 agents (10 deals each): ~$25,177/year.

**Option B: Flat Fee Per Listing (No Split)**

| Price Point | Agent Pays | Brokerage Profit/Listing | Profit at 5 Agents (50 listings) |
|---|---|---|---|
| $500/listing | $500 | $179 | $8,950 |
| $750/listing | $750 | $429 | $21,450 |
| $1,000/listing | $1,000 | $679 | $33,950 |

No commission split. Agent keeps 100%. Pays per use.

**Key Consideration:** ROG Authentic is a fee-based brokerage, not a split-based model. The flat fee option aligns with brand identity. The $750 price point delivers comparable profit to the 10% split while keeping the "keep what you earn" message intact.

---

## The Launch Plan

The Launch Plan is the core system. It's a physical tri-fold document agents fill out with clients at listing appointments. The conversation follows a backwards-planning method from listing date, securing 5 agreements naturally:

1. **Open House** - First Saturday/Sunday after listing
2. **Photography** - 4 days before listing (4-5:30pm)
3. **Cleaning** - Morning of photography day
4. **Listing Warranty** - Starts on listing date
5. **Listing Paperwork** - Delivered within 24-48 hours

After the appointment, the agent photos the completed Launch Plan, puts the original on the client's fridge, and submits the Listing Launch form with the photo attached. The team handles everything from there.

Training guide: [launch-plan-training-guide.html](./training/launch-plan-training-guide.html)

---

## Operations Architecture

### Data Flow

```
Agent submits form (OpnForm)
        │
        ▼
Zapier Trigger (New Submission)
        │
        ▼
Google Sheets (Master Tracker)
   ├── Raw Pre-Listing tab (Zap 1)
   ├── Raw Buyer TC tab (Zap 2)
   ├── Pre-Listing Tracker tab (formulas reference Raw tab)
   ├── Buyer TC Tracker tab (formulas reference Raw tab)
   └── Dashboard tab (formulas reference both Tracker tabs)
        │
        ▼
VA opens tracker → sees new row → starts services
```

### Zapier Setup

**Zap 1: Pre-Listing**
- Trigger: OpnForm → New Form Submission → Pre-Listing form
- Action: Google Sheets → Create Spreadsheet Row → Master Tracker → "Raw Pre-Listing" tab

**Zap 2: Buyer TC**
- Trigger: OpnForm → New Form Submission → Buyer TC form
- Action: Google Sheets → Create Spreadsheet Row → Master Tracker → "Raw Buyer TC" tab

Two zaps. Two steps each. No formatters, no ChatGPT parsing, no paths.

### Form Fields (Pre-Listing)

| Step | Fields |
|---|---|
| 1. Agent Info | Name, Phone, Email |
| 2. Property | Address, List Price, Target List Date |
| 3. Seller Info | First Name(s), Last Name, Phone, Email |
| 4. Access | Lockbox/Access, Showing Availability, Notes |
| 5. Paperwork | Docs Completed (dropdown), Total Comm %, BAC |
| 6. Services | Display-only (all 8 auto-included) |
| 7. Notes + Upload | Special Notes, Launch Plan upload (required) |

Hidden field: `form_type = "pre_listing"`

### Tracker Features

- All 8 service columns auto-fill "Yes" on every submission (no selection needed)
- Status dropdowns: New, In Progress, Waiting on Agent, Completed, On Hold
- VA assignment dropdowns per row
- Dashboard with live counts across both trackers
- Seller first + last name auto-combined via formula

---

## Recruiting

### Target Personas

| Persona | Profile | Trigger |
|---|---|---|
| **The Grinder** | 8-10 deals, 60+ hrs/week, does everything solo | Missing kid's game due to closing chaos |
| **The Plateaued Producer** | 11-14 deals, stuck 3 years | Knows leverage is the answer, can't afford a hire |
| **The Big Box Refugee** | Paying 25-30% split, getting nothing | Watching commission disappear monthly |
| **The Team Curious** | Approached by teams, wants infrastructure | Doesn't want 40-50% split or loss of independence |
| **The Inconsistent Marketer** | Last social post 3 weeks ago | Past client listed with someone else |
| **The Scaling Newbie** | Just hit 8 deals, fragile momentum | Needs systems before bad habits form |

Common thread: *"I'm good enough to sell more, but something is holding me back."* That something is always operations, never talent.

### Teaser Campaign (Feb 19 - Mar 3, 2026)

Two weeks of cryptic social posts + emails building to the March 3 reveal.

| Date | Post | Type |
|---|---|---|
| Feb 19 | "Something Is Coming" | Static image |
| Feb 21 | "You're Not Bad at This Business" | Static image |
| Feb 24 | "We've been building something" | Video (30-45 sec) |
| Feb 24 | Email #1 to both lists | Email |
| Feb 26 | "85% of Your Time" | Static image |
| Feb 28 | "Three days. March 3rd." | Video (20-30 sec) |
| Feb 28 | Email #2 (current agents) | Email |
| Feb 28 | Email #3 (recruiting prospects) | Email |
| Mar 2 | "Tomorrow. You Sell. We Launch." | Static image |
| Mar 3 | **REVEAL** - Landing page goes live | All channels |

---

## Tech Stack

| Tool | Purpose |
|---|---|
| **OpnForm** | Agent submission forms (pre-listing + buyer TC) |
| **Zapier** | Routes form submissions to Google Sheets |
| **Google Sheets** | Master Tracker with dashboard |
| **Google Docs/Sites** | SOP Playbook (planned) |
| **Custom GPT/Gem** | AI assistant trained on SOPs (planned) |
| **GitHub** | Asset source code repository |
| **joinrogauthentic.com** | Main recruiting website |

---

## Pending

- [ ] Buyer TC form (OpnForm prompt)
- [ ] Landing page for March 3 reveal
- [ ] SOP Playbook for VAs
- [ ] AI Assistant (Custom GPT/Gem) trained on SOPs
- [ ] Remaining teaser posts (2-6)
- [ ] Email campaign copy (reveal day)
- [ ] Fee-based pricing tier for non-ONE & Done agents

---

## Contact

**Scott Bergmann**
Broker/Owner, Realty ONE Group Authentic
National AI Coach, Realty ONE Group

- [joinrogauthentic.com](https://joinrogauthentic.com)
- [tidycal.com/scottb](https://tidycal.com/scottb/schedule-a-phone-call-broker)

---

*Built with obsessive attention to detail and zero corporate energy.*
