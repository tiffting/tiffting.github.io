---
layout: case-study
title: Capisara Platform
tagline: Unified box office management across multiple sales channels
category: MVP Development
role: Product Manager & Full-Stack Developer
timeline: June 2025 - Present
tech_stack: React 18, TypeScript, Vite, Tailwind CSS, Supabase, Square API
links:
  - title: Landing page
    url: https://capisara.com/
published: true
---

## Challenge

Comedy venues selling tickets through multiple channels face a critical operational problem: managing inventory across platforms without creating cognitive load for staff. Existing solutions lock organizers into single platforms, preventing flexible multi-channel sales.

**The specific pain point:** Venues running multiple shows per day (e.g., 8pm and 10pm) need box office staff to manually select the correct ticket variant in their POS system—even when only one option makes sense (single-show nights, or after the first show has already ended). This creates unnecessary friction and potential for human error during high-pressure sales moments.

![Box office staff must choose between 8PM and 10PM variants even after 8PM show has ended]({{site.baseurl}}/images/case_studies/capisara/square-scheduler/pos-before.gif)

### User Story: Jamie the Producer

Jamie manages comedy shows and spends 15+ hours per week on operational tasks. She struggles with:
- Managing inventory across Eventbrite, direct sales, and door sales from a single ticket pool
- Manually coordinating which Square POS variants are available at which times
- Reconciling sales data across disconnected systems
- Training box office staff on time-sensitive variant selection rules

**Goal:** Reduce operational overhead from 15+ hours to 5 hours per week while eliminating manual coordination tasks.

## Solution

**Capisara** is a unified box office management system that automates multi-channel inventory coordination. The platform prioritizes reducing cognitive load for venue staff through intelligent automation.

### In Production Now

**Automated Square Inventory Management:** A multi-tenant scheduling system automatically enables/disables ticket variants based on organization-specific rules stored in the database.

**Impact:**
- **Before:** Producer manually updated variant availability twice per show day
- **After:** Zero manual updates—system handles it automatically
- **Staff experience:** Box office sees only the relevant ticket variant(s) for the current time, eliminating decision-making overhead

![Scheduler automatically hides irrelevant variants, removing decision overhead]({{site.baseurl}}/images/case_studies/capisara/square-scheduler/pos-after.gif)

**Technical implementation:**
- Multi-tenant Supabase Edge Function triggered hourly by external cron service (cron-job.org)
- Database-driven scheduling rules: each organization defines day-of-week and time-based patterns in `channel_policies`
- Encrypted credential storage: Square API keys per-organization via Supabase Vault
- Email notifications with consolidated results across all organizations
- Handles multiple patterns: single-show nights, dual-show nights, post-show cutoffs

![Automated monitoring: consolidated email alerts show actions across all organizations]({{site.baseurl}}/images/case_studies/capisara/square-scheduler/email.png)

### Architectural Foundation

**Multi-tenant from day one** (proven in production):
- **Working multi-tenancy:** Square scheduler processes multiple organizations with isolated credentials and independent scheduling rules
- **Database schema:** PostgreSQL with Row Level Security for organization isolation
- **Secure credential storage:** Supabase Vault for encrypted per-organization API keys
- **Channel architecture pattern:** Extensible design ready for additional integrations (Eventbrite, Ninkashi)
- **Mobile-first UI:** Check-in interface architected for tablet-based venue staff (awaiting data source)

**Multi-Tenant Architecture Flow:**

1. **cron-job.org** triggers edge function every hour at :40

2. **Supabase Edge Function** queries PostgreSQL database for all organizations with Square integration enabled

3. **For each organization**, process independently:
   - Read scheduling rules from database (`channel_policies`)
   - Decrypt Square credentials from Supabase Vault (access token, app ID, location ID)
   - Evaluate current time against organization's scheduling rules
   - Execute Square API calls to enable/disable variants based on rules

4. **Send consolidated email report** with results from all organizations:
   - ✅ CTT Comedy: 2 actions executed
   - ⚪ Org 2: no actions needed
   - ✅ Org 3: 1 action executed

## Development Process

### Phase 1: User Research & Problem Definition
- Interviewed 3 venue organizers and 2 box office staff members
- Identified cognitive load reduction as primary opportunity
- Validated multi-channel coordination as core pain point
- Researched external platform APIs (Facebook Events, Google Business Profile both hit dead ends due to API restrictions)

### Phase 2: Production Deployment (Square Automation)
- Evaluated AI development tools (4 iterations on Lovable, 1 on Bolt) before selecting Claude Code for production implementation
- Rebuilt from scratch with Claude Code for code quality, architectural discipline, and control
- Designed intelligent variant selection logic with database-driven configuration
- Implemented time-based automation with email notifications
- Deployed to production and validated real-world impact
- Refined edge case handling based on actual usage patterns

![CTT Comedy's automated schedule: variants enabled/disabled based on show timing patterns]({{site.baseurl}}/images/case_studies/capisara/square-scheduler/cal.png)

### Phase 3: Check-in System Architecture (In Progress)
- Designed mobile-first tablet interface for venue staff
- Built channel abstraction layer for future integrations
- Multi-tenant database with Row Level Security implemented
- **Current blocker:** Awaiting external ticketing platform API (Ninkashi) to provide transaction data

## Key Learnings

### Technical Execution
- **Ship working code first:** Getting Square automation to production built stakeholder trust and validated the approach, even as a small piece of the larger vision
- **Production teaches:** Real-world usage revealed edge cases (day-of-week rules, post-show cutoffs) that weren't obvious in planning
- **Tool selection matters:** No-code platforms (Lovable, Bolt) hit limits transitioning from prototype to production-ready code. Claude Code provided the code quality, architectural discipline, and control needed for production systems
- **API research pays off:** Early evaluation of Facebook Events and Google Business Profile APIs saved weeks of wasted integration effort
- **Infrastructure pragmatism:** GitHub Actions proved unreliable for time-sensitive jobs (30+ minute delays, missed runs). Switched to external cron service (cron-job.org) for production reliability, accepting the tradeoff of manual schedule configuration

### Product Strategy
- **Start with pain:** Automating manual variant updates solved an immediate, tangible problem—building momentum for larger features
- **User validation matters:** Prototype feedback from 5 real users (3 organizers, 2 staff) shaped priorities and caught assumptions
- **External dependencies are risk:** The check-in system's core value is blocked by a partner API—architectural readiness doesn't ship features

### Architecture vs. Execution
- **Multi-tenant from day one** was correct—proven in production with Square scheduler handling multiple organizations with isolated credentials
- **Database-driven configuration** enables rapid onboarding: new organizations just need database records, no code changes
- **Channel pattern** adds upfront complexity but enables extensibility—Square working, Eventbrite/Ninkashi ready to integrate
- **Mobile-first thinking** influenced database design (offline-first patterns, simplified data models)

## Current Status

**In Production:**
- Square POS variant automation serving real venue operations

**Architecturally Ready:**
- Mobile check-in interface
- Multi-tenant database infrastructure
- Channel integration framework

**Blocked:**
- Core check-in functionality awaiting Ninkashi API development (external dependency)

## Next Steps

**Immediate** (pending Ninkashi API availability):
- Deploy mobile check-in system with transaction data integration
- Multi-venue dashboard for producers managing multiple locations
- Real-time capacity tracking across all sales channels

**Future enhancements:**
- Multi-tenant scheduling infrastructure (Square automation currently single-organization)
- Customer self-service portal for transfers and refunds
- Automated financial reconciliation across channels
- Business intelligence and analytics dashboard
- Additional ticketing platform integrations (Eventbrite, others)
