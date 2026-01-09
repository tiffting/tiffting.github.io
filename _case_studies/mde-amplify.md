---
layout: case-study
title: AMPLIFY
tagline: Connecting artists to grassroots climate action
category: Product Strategy & Systems Design
role: Product Strategist & UX Researcher
timeline: October 2025 - Present
tech_stack: ChatGPT (research synthesis), Cloudflare Workers (planned)
links:
  - title: Music Declares Emergency
    url: https://www.musicdeclares.net/
  - title: AMPLIFY Program
    url: https://www.musicdeclares.net/us/campaigns/mde-us-amplify-program
published: true
---

## Challenge

Artists want to mobilize their fans around climate action, but face significant barriers:

- **Risk aversion**: Fear of losing shows, alienating promoters, or becoming politically polarized
- **Coordination complexity**: International tours cross dozens of cities and countries, each needing local climate organizations
- **Knowledge gaps**: Artists aren't climate experts and don't have time to research trustworthy organizations
- **Tour fatigue**: Consistency breaks down under the demands of travel and performance

**The core problem**: How do you design a program that enables participation without courage, context, or coordination?

## Origin Story

In October 2025, I attended a Garbage concert at The Warfield on a whim. At the venue, Pete Kronowitt was tabling for Music Declares Emergency (MDE), promoting HeadCount—a voter registration nonprofit that Garbage had chosen to support. The organization's slogan caught my attention: **"No music on a dead planet."**

After chatting with Pete about MDE's mission and their AMPLIFY program (connecting touring artists with local grassroots climate organizations), I became interested in contributing my product and UX skills to a meaningful cause. We met for brunch the following week, and I attended my first team standup from his home in San Francisco.

Despite having no expertise in the music industry or climate action, I saw an opportunity to apply strategic product thinking to an underserved problem space.

## User Research: Discovering the Real Constraints

Working with Pete, I conducted two in-depth interviews with artist managers to understand their perspective on climate advocacy:

### Interview 1 with Alex (Manager): Ceiling Case
- Activism is identity-level for their artist
- Manager designs and runs systems
- Fans expect political engagement
- High effort, high conviction, low fear

**Key insight**: This level of engagement does not scale.

### Interview 2 with Lara (Booking Agent + Artist): Baseline Reality
- Artists care but are risk-averse
- Fear of lost shows is rational
- Logistics + ambiguity kill follow-through
- Survival economics take precedence over values under pressure

**Key insight**: This must be the design baseline.

### Research Synthesis: What Actually Scales

Across both interviews, a clear pattern emerged:

**Artists will reliably do:**
- Share a single QR code
- Play a short pre-show video (≤5 minutes)
- Allow passive fan action
- Add light endorsement if safe

**Artists will NOT reliably do:**
- Speak onstage every night
- Educate audiences
- Customize messaging per city
- Commit tour-wide
- Take reputational or booking risks

**The design principle**: If AMPLIFY requires bravery, education, or ongoing coordination, it will fail quietly.

## Strategic Contributions

### 1. MOU Restructuring: Separating Contracts from Guidelines

When Pete shared a draft Memorandum of Understanding (MOU) with partner organizations, I identified that it was trying to do too many things at once: legal protection, operational expectations, program guidelines, and quality standards all in one document.

**My approach** (using ChatGPT as a thought partner since I'd never written an MOU):

1. **Asked first-principles questions**:
   - What specifically counts as an organization "screw-up"?
   - What's MDE's expected response, and how quickly?
   - What are orgs required to do vs. encouraged to do?
   - What happens if expectations aren't met?

2. **Identified the core issue**: The MOU needed to protect artists and give MDE authority to act, but operational guidelines needed flexibility to evolve.

3. **Proposed a separation of concerns**:
   - **MOU**: Tight, legal-style document focusing on guardrails, minimum obligations, and termination conditions
   - **Partner Organization Guidelines**: Non-legal, operational document covering tone, action quality, expectations for artist-facing contexts

**Impact**: Pete's response: "I absolutely loving your feedback. You are definitely thinking about things that could potentially trip us up."

The separation reduced perceived risk for artists, set clearer expectations for partner orgs, and gave AMPLIFY room to function as reliable infrastructure.

### 2. Evergreen Link System: The Technical Insight

During a team standup, I had been focusing on the wrong question: "Would artists participate in AMPLIFY if we made it low-effort enough?"

Pete clarified that he already knows some artists will participate (and he has examples). What he needs is an MVP that works for **internationally touring artists**, potentially including a major artist tour in 2026.

**The problem**: Artists tour internationally, but effective climate action is local. How do you create a simple, artist-friendly system that connects fans to the right organization based on location?

**The solution**: An evergreen artist link with intelligent routing.

**Architecture**:
1. **Artist receives a single, permanent link**: `amplify.musicdeclares.net/{artist-slug}`
2. **Link works everywhere**: Social media, QR codes on stage screens, printed materials
3. **Router determines context**: When a fan clicks, the system checks:
   - Does this artist exist?
   - Is their tour active today?
   - Can we determine the fan's country from IP geolocation?
   - Do we have a partner organization for this artist + country?
4. **Redirect to relevant organization**: 302 redirect with UTM tracking parameters
5. **Fallback for edge cases**: If context can't be determined, redirect to AMPLIFY general page

![System diagram showing evergreen link routing logic]({{site.baseurl}}/images/case_studies/mde_amplify/mvp-system-diagram.png)

**Why this matters**:
- **Zero artist maintenance**: Link never changes, works across all platforms
- **Data-driven learning**: Captures artist, tour dates, location, organization, and timestamp (no PII)
- **Proves impact**: Both at program level and per-artist for reporting
- **Scalable**: Adding new artists or organizations is just configuration, not code changes

Pete's reaction: "I'm absolutely floored by this proposal. It is so straightforward: well done."

## Technical Implementation

**MVP Scope** (April 2026 launch target):
- Cloudflare Worker for routing logic
- IP-based geolocation
- Simple admin interface for tour configuration (dates, countries, selected orgs per country)
- Analytics tracking (non-PII)
- 302 redirects with UTM parameters

**Success metrics**:
- Zero technical difficulties with artist links
- Artists actually use links (social posts, QR codes, stage screens)
- Modest clickthrough rate
- At least one pilot artist before major tour partnership

## Working in Unfamiliar Territory

This project required navigating domains where I had no prior expertise:

### Using ChatGPT as Mentor
Rather than just asking for outputs, I used ChatGPT to:
- **Develop interview questions** that wouldn't lead to rambling
- **Analyze legal documents** I'd never encountered before (MOUs)
- **Ask clarifying questions** about music industry norms and climate action frameworks
- **Validate concerns** before raising them with the team

This "AI as thought partner" approach allowed me to contribute meaningfully despite knowledge gaps.

### First-Principles Thinking
When reviewing the MOU, I didn't have legal expertise—but I could ask:
- What is this document trying to accomplish?
- Who is it protecting, and from what risks?
- What needs to be rigid vs. flexible?
- How will this scale as the program grows?

This approach led to the MOU/guidelines separation that Pete and the team valued.

### Reality Checks and Anticipatory Thinking
Pete specifically appreciated my ability to:
- Surface concerns others weren't raising
- Identify potential failure modes
- Think through second-order effects (e.g., "What happens if an org has a PR scandal after an artist promotes them?")

## Current Status

**Completed:**
- User research with 2 artist managers
- Research synthesis identifying design constraints
- MOU restructuring (legal + operational guidelines)
- System architecture for evergreen link routing
- MVP scope definition

**In Progress:**
- Building AMPLIFY Router (Cloudflare Worker)
- Recruiting pilot artists
- Partner organization vetting and agreements

**Launch Target:** April 2026

## Key Learnings

### Strategic Product Thinking
- **Research reveals constraints, not just preferences**: The "participation without courage" insight became the entire product strategy
- **Separate contracts from operations**: Legal documents need different properties than living guidelines
- **Design for exhaustion**: If your users are tired, stressed, and cautious, the system must work anyway

### Working Outside Expertise
- **AI as thought partner scales your capabilities**: ChatGPT let me navigate unfamiliar domains (music industry, legal documents, climate action) by providing context and asking better questions
- **First-principles thinking transfers across domains**: Even without domain knowledge, you can identify core problems and propose solutions by asking "what is this actually trying to accomplish?"
- **Ask the questions others aren't asking**: Sometimes the most valuable contribution is surfacing concerns and edge cases

### Systems Design
- **Evergreen infrastructure reduces friction**: One link that never changes is better than dynamic links that need constant updates
- **Routing intelligence enables scale**: Let the system handle complexity (geolocation, context resolution) so artists can stay simple
- **Design for data from day one**: Analytics aren't just reporting—they're how you learn and improve

### Nonprofit Constraints
- **Mission-driven work attracts talent**: The chance to contribute skills to climate action was compelling enough to volunteer
- **Small teams need decisive contributions**: In a volunteer-driven organization, thorough analysis and clear proposals have outsized impact
- **Pro bono work is still product work**: The same principles apply—user research, systems thinking, measuring impact

## Potential Impact

If AMPLIFY reaches its goals:
- **Pilot phase**: 1-3 artists testing the system
- **Scale target**: 80 artists participating
- **Fan reach**: Millions of fans directed to local climate organizations
- **Validation metric**: Geolocation accuracy across 20+ countries

This program could become replicable infrastructure for connecting artists (or any public figures with touring audiences) to local action organizations across causes.

## What's Next

**Immediate** (Pre-launch):
- Complete AMPLIFY Router implementation
- Finalize partner organization agreements
- Create action kit assets (QR codes, graphics, video templates)
- Recruit and onboard pilot artists

**Post-MVP**:
- More granular routing (by city, by show)
- Artist self-service configuration tools
- Analytics dashboards for artists and MDE
- Standardized tracking integrations with partner organizations
- Governance and override controls for edge cases
