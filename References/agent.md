# AI Agent File Management Specifications

**Purpose:** Technical specifications for managing files, properties, links, and templates in Fachry's dual-brand knowledge vault.

**Scope:** This document contains ONLY operational rules. For strategic decisions, check `References/README.md` and `Unified Strategy 2026.md`.

---

## FOLDER STRUCTURE

```
vault/
├── /                        # Vault root - Fachry's original work lives here
├── References/              # External entities (tools, people, frameworks)
├── Clippings/              # Saved content from others
├── Builds/                 # Completed apps/projects
├── Daily/                  # Date anchors (YYYY-MM-DD.md)
├── Attachments/           # Media files
├── Templates/             # Templates only
└── Bases/                 # Obsidian plugin data (.base files)
```

**NOTE:** Original content goes directly in the vault root (`/`), NOT in a folder called "Root/".

**RULES:**
- NO subfolders allowed in any folder
- NO nested hierarchies
- Flat structure only
- Use properties for categorization
- **EXCEPTION:** `Bases/` folder is allowed for Obsidian plugin compatibility

---

## FILE PLACEMENT ALGORITHM

**Execute this decision tree for EVERY new file:**

```
INPUT: New note to create

┌─ STEP 1: Classification ─────────────────────────────────┐
│ Q: "Did Fachry create this content originally?"          │
│ ├─ YES → STEP 2                                          │
│ └─ NO  → STEP 3                                          │
└───────────────────────────────────────────────────────────┘

┌─ STEP 2: Original Content ───────────────────────────────┐
│ Q: "Is this a completed, shipped app/project?"           │
│ ├─ YES → Place in Builds/                                │
│ │        Add build properties                            │
│ │        Add to Daily note                               │
│ │                                                         │
│ └─ NO  → Place in vault root (/)                         │
│          Add content properties                          │
│          Add to Daily note                               │
└───────────────────────────────────────────────────────────┘

┌─ STEP 3: External Content ───────────────────────────────┐
│ Q: "Is this about a tool, person, or framework?"         │
│ ├─ YES → Place in References/                            │
│ │        Add reference properties                        │
│ │                                                         │
│ └─ NO  → STEP 4                                          │
└───────────────────────────────────────────────────────────┘

┌─ STEP 4: Saved Content ──────────────────────────────────┐
│ Q: "Is this article/video from someone else?"            │
│ ├─ YES → Place in Clippings/                             │
│ │        Add research properties                         │
│ │                                                         │
│ └─ NO  → STEP 5: Specialized Content                     │
└───────────────────────────────────────────────────────────┘

┌─ STEP 5: Specialized Content ────────────────────────────┐
│ Q: "Is this a Prompt or a Profile?"                       │
│ ├─ YES → Place in References/                            │
│ │        Add reference properties                        │
│ │                                                         │
│ └─ NO  → STEP 6: ERROR HANDLING                          │
└───────────────────────────────────────────────────────────┘

┌─ STEP 6: Error Handling ─────────────────────────────────┐
│ → STOP                                                    │
│ → ASK: "Is this YOUR work, an EXTERNAL reference,        │
│         or SAVED content from others?"                    │
│ → WAIT for clarification                                 │
│ → NEVER guess folder placement                           │
└───────────────────────────────────────────────────────────┘

┌─ STEP 7: Validation ─────────────────────────────────────┐
│ BEFORE creating file, verify:                            │
│ ✓ Folder placement correct per decision tree?            │
│ ✓ Properties block complete for note type?               │
│ ✓ Filename follows naming convention?                    │
│ ✓ Related notes searched and linked?                     │
│                                                           │
│ IF all YES → CREATE file                                 │
│ IF any NO  → STOP → FIX → THEN CREATE                    │
└───────────────────────────────────────────────────────────┘
```

---

## FILENAME CONVENTIONS

**Vault root files:**
```
Format: [Optional: YYYY-MM-DD HHMM] Title with spaces.md

Examples:
✅ 2025-01-15 1045 AI agent file management idea.md
✅ Kamal Way Week 1 module script.md
✅ Why AI wont replace thinking - essay.md
✅ Invoice generator product spec.md

❌ Week 1/Script.md (no folders)
❌ kamal_way_script.md (use spaces not underscores)
❌ script-v2-final-FINAL.md (no version numbers)
```

**References/ files:**
```
Format: Title Case.md

Examples:
✅ Claude Code.md
✅ Pieter Levels.md
✅ First Principles Thinking.md

❌ claude-code.md (use Title Case)
❌ tools/Claude Code.md (no folders)
```

**Clippings/ files:**
```
Format: Original Title.md

Examples:
✅ The Future of AI Coding - MIT Review.md
✅ How Pieter Levels Built 12 Startups.md

❌ article-1.md (use original title)
❌ saved-article.md (use original title)
```

**Builds/ files:**
```
Format: Descriptive Name Build.md

Examples:
✅ Invoice Generator Build.md
✅ Pomodoro Timer Build.md
✅ Habit Tracker Build.md

❌ Build 1.md (use descriptive name)
❌ invoice-generator.md (add "Build" suffix)
```

**Daily/ files:**
```
Format: YYYY-MM-DD.md (STRICT)

Examples:
✅ 2025-01-15.md
✅ 2025-12-31.md

❌ 15-01-2025.md (wrong format)
❌ Jan 15 2025.md (wrong format)
❌ 2025-01-15 Monday.md (date only)
```

**Templates/ files:**
```
Format: Template Name Template.md

Examples:
✅ Content Idea Template.md
✅ Product Spec Template.md
✅ Build Note Template.md

❌ content-template.md (use Title Case)
❌ Template.md (needs specific name)
```

---

## PROPERTY SYSTEM

**CRITICAL RULE:** Every note MUST have properties block at top.

### Standard Properties (All Notes)

```yaml
---
type: [required - from allowed types]
status:
  - "[[Required Status]]"
brand: [required for content/products - kamal/freebuilder/fachry]
created: 
  "{ date }":
tags:
  - [tag1]
  - [tag2]
related:
  - - [[Note Link]]
---
```

**Allowed `type` values:**
- `content-idea` - Idea for video/post/article
- `script` - Video or podcast scripts (Long/Short form)
- `caption` - Social media caption
- `product-spec` - Product specification
- `product-idea` - Product idea
- `build` - Completed app/project
- `research` - Research note
- `clipping` - Saved article/video
- `reference` - External entity note
- `essay` - Long-form writing (Articles/Essays)
- `prompt` - AI system instructions or persona prompts
- `profile` - Detailed entity descriptions (Person/Brand/ICP)
- `daily` - Daily note
- `review` - Monthly/weekly review

**Allowed `status` values (Must be wikilinked):**
- `[[Idea]]` - Initial capture
- `[[Active]]` - In progress
- `[[Published]]` - Live/shipped
- `[[Archived]]` - No longer active
- `[[Validating]]` - Testing demand
- `[[Building]]` - In development
- `[[Launched]]` - Product live
- `[[Working]]` - App functional
- `[[Broken]]` - App needs fixing

**Allowed `brand` values:**
- `kamal` - The Kamal Way content/product (Career/Systems)
- `freebuilder` - Freebuilder content/product (Building/AI Tools)
- `fachry` - Unified Personal Brand (The Hybrid Leader)

### Content Production Properties

```yaml
---
type: [content-idea, script, caption]
status: [idea, scripting, ready, published]
brand: [kamal, freebuilder, both]
platform: [youtube, tiktok, linkedin, twitter, instagram]
content-pillar: [ai, future-of-work, coding-with-ai, systems-thinking, career-growth]
hook: "Opening 3 seconds"
cta: "Call to action"
publish-date: YYYY-MM-DD
performance: [views, engagement-rate]
related: []
---
```

**When to use:**
- Vault root files that are video scripts, captions, or content ideas
- Any content meant for publishing

**Example:**
```yaml
---
type: script
status: ready
brand: freebuilder
platform: [tiktok, youtube-shorts]
content-pillar: coding-with-ai
hook: "I built this in 60 seconds"
cta: "Link in bio for 30-day challenge"
publish-date: 2025-01-20
performance: []
related: [[Invoice Generator Build], [Day 12 Freebuilder]]
---
```

### Product Development Properties

```yaml
---
type: [product-idea, product-spec, build]
status: [idea, validating, building, launched, archived]
brand: [kamal, freebuilder, both]
product-type: [course, saas, community, service, digital-product]
revenue-model: [one-time, recurring, free]
validation: [yes, no, in-progress]
launch-date: YYYY-MM-DD
price: 
mrr: 
related: []
---
```

**When to use:**
- Vault root files for product specs or ideas
- NOT for builds (they use build properties)

**Example:**
```yaml
---
type: product-spec
status: validating
brand: kamal
product-type: course
revenue-model: one-time
validation: in-progress
launch-date: 2025-02-01
price: 1500000
mrr: 0
related: [[Kamal Week 1 Script], [ICP Interview Notes]]
---
```

### Research Properties

```yaml
---
type: [research, clipping]
source: [URL or publication]
author: 
created: YYYY-MM-DD
rating: [1-7]
key-insights: []
content-ideas: []
tags: []
related: []
---
```

**When to use:**
- Clippings/ files (saved articles, videos)
- Vault root files that are research synthesis

**Example:**
```yaml
---
type: clipping
source: https://example.com/article
author: John Doe
created: 2025-01-15
rating: 6
key-insights: [ai-assistants-work-best-with-specs, free-tools-compete-with-paid]
content-ideas: [[Freebuilder Day 20 idea], [Why specs matter essay]]
tags: [ai, coding-with-ai]
related: [[Claude Code], [Cursor Comparison]]
---
```

### Build Properties

```yaml
---
type: build
brand: [kamal, freebuilder, both]
build-date: YYYY-MM-DD
tools-used: []
build-time: "X hours"
demo-url: 
github-url: 
status: [working, broken, archived]
monetized: [yes, no]
revenue: 
featured-in: []
related: []
---
```

**When to use:**
- ONLY for Builds/ folder files
- Completed apps/projects

**Example:**
```yaml
---
type: build
brand: freebuilder
build-date: 2025-01-12
tools-used: [claude-code, cursor, replit]
build-time: "2 hours"
demo-url: https://invoice-gen.example.com
github-url: https://github.com/fachry/invoice-gen
status: working
monetized: no
revenue: 0
featured-in: [[Day 12 Freebuilder Script], [Portfolio Page]]
related: [[Invoice Generator Spec]]
---
```

### Reference Properties

```yaml
---
type: reference
reference-type: [tool, person, framework, platform, concept]
url: 
created: YYYY-MM-DD
tags: []
related: []
---
```

**When to use:**
- References/ folder files only
- External entities (not Fachry's original work)

**Example:**
```yaml
---
type: reference
reference-type: tool
url: https://claude.ai
created: 2025-01-10
tags: [ai, coding, tools]
related: [[Builds using Claude Code], [Claude vs Cursor essay]]
---
```

### Daily Note Properties

```yaml
---
type: daily
created: YYYY-MM-DD
---
```

**When to use:**
- Daily/ folder files ONLY
- Minimal properties required

---

## PROPERTY VALIDATION CHECKLIST

**Before creating/updating any note:**

```
✓ Properties block exists at top?
✓ `type` is from allowed types list?
✓ `status` matches the `type`?
✓ `brand` specified for content/products?
✓ `created` date in YYYY-MM-DD format?
✓ `related` property exists (even if [])?
✓ All type-specific properties included?
✓ Property values use kebab-case?
✓ Array properties use [] format?

IF any NO → STOP → FIX → THEN save
```

---

## LINKING STRATEGY

### When Creating New Note

```
STEP 1: Search for related notes
  → Search by keywords in title
  → Search by tags if relevant
  → Search by content-pillar if content note

STEP 2: Add wikilinks in body
  Format: [[Exact Note Title]]
  
  Examples:
  ✅ [[Invoice Generator Build]]
  ✅ [[Kamal Way Week 1 Script]]
  ❌ [[invoice-generator]] (wrong - use title)
  ❌ [[Week 1]] (ambiguous - use full title)

STEP 3: Update related property
  Add bidirectional links:
  related: [[Note A], [Note B], [Note C]]

STEP 4: Create unresolved links as breadcrumbs
  IF concept mentioned but note doesn't exist:
  → Create [[Unresolved Link]]
  → This signals "create this note later"
```

### Link Types by Note Type

**Content notes → Link to:**
- Research that inspired it
- Products to mention
- Related content pieces
- Builds featured in content

**Product notes → Link to:**
- Content created for launch
- Research that validated it
- Related products
- Build if product includes software

**Build notes → Link to:**
- Content featuring the build
- Product specs (if build is for product)
- Research/tools used
- Related builds

**Research notes → Link to:**
- Content ideas triggered
- Related research
- Products this validates
- Builds this inspired

### Linking Rules

```
✓ DO:
  - Link when connection is meaningful
  - Use exact note titles
  - Update related: [] property
  - Create unresolved links for future notes

✗ DON'T:
  - Link for sake of linking
  - Link to Daily notes (Daily links TO notes, not reverse)
  - Create ambiguous links
  - Use shortened/abbreviated titles
```

---

## DAILY NOTE MANAGEMENT

### Daily Note Format (STRICT)

```markdown
---
type: daily
created: YYYY-MM-DD
---

# YYYY-MM-DD

## Captured today
- [[Note Created 1]]
- [[Note Created 2]]

## Worked on
- [[Note Edited 1]]
- [[Note Edited 2]]

## Published
- [[Content Published 1]]

## Notes
Brief context (2-3 sentences max)
```

**RULES:**
- Daily notes are LINKS ONLY
- NO content written in daily notes
- NO property blocks except type and created
- Brief notes section allowed (max 3 sentences)
- Create new daily note when day changes

### Daily Note Automation

```
WHEN user creates note:
  → Add link to Daily/YYYY-MM-DD.md under "Captured today"

WHEN user says "published X":
  → Add link to Daily/YYYY-MM-DD.md under "Published"
  → Update note status to "published"
  → Add publish-date property

WHEN user says "working on X":
  → Add link to Daily/YYYY-MM-DD.md under "Worked on"
  → Update note status if needed
```

---

## TEMPLATE SYSTEM

### Template Usage Rules

```
WHEN user says "create [type] note":
  → Use appropriate template from Templates/ folder
  → Fill in properties with current date
  → Place in correct folder per decision tree
  → Prompt user for required information
  → Save when complete

NEVER create notes without using templates
```

### Template Definitions

**1. Content Idea Template**
```yaml
---
type: content-idea
status: idea
brand: 
platform: []
content-pillar: 
created: YYYY-MM-DD
related: []
---

# [Content Title]

## Hook (Problem/Pattern)


## Core Message


## Why This Matters


## Format Ideas
- Short video
- Thread
- Essay
- Tutorial

## Related
- Research: 
- Products: 
- Previous content: 
```

**2. Script Template**
```yaml
---
type: script
status: drafting
brand: 
platform: 
content-pillar: 
hook: 
cta: 
created: YYYY-MM-DD
related: []
---

# [Video Title]

## Hook (0-3s)


## Setup (3-15s)


## Main Content (15-50s)


## Proof/Demo (50-70s)


## CTA (70-90s)


## Production Notes
- B-roll:
- Graphics:
- Tools to show:
```

**3. Caption Template**
```yaml
---
type: caption
status: drafting
brand: 
platform: 
for: [[linked script]]
created: YYYY-MM-DD
related: []
---

# Caption for [Video]

## TikTok/Reels


## YouTube


## Twitter/X


## LinkedIn
```

**4. Product Spec Template**
```yaml
---
type: product-spec
status: idea
brand: 
product-type: 
revenue-model: 
validation: no
price: 
created: YYYY-MM-DD
related: []
---

# [Product Name]

## Problem (3P Framework)
- Pervasive:
- Precise:
- Persistent:

## Solution


## Target Customer


## Offer Structure
- What they get:
- Timeframe:
- Price:
- Guarantee:

## Validation Plan
- Who to ask:
- Success criteria:

## Content Strategy
- Launch content:
- Ongoing content:
```

**5. Build Note Template**
```yaml
---
type: build
brand: 
build-date: YYYY-MM-DD
tools-used: []
build-time: 
demo-url: 
github-url: 
status: working
monetized: no
related: []
---

# [Build Name]

## What It Does


## Tech Stack
- AI tools:
- Deployment:
- Database:

## Build Process
- Time taken:
- Challenges:
- Learnings:

## Monetization
- Used in service:
- Featured in content:
- Could become product:

## Prompts Used
```prompts
[Paste key prompts]
```
```

**6. Research Clip Template**
```yaml
---
type: clipping
source: 
author: 
created: YYYY-MM-DD
rating: 
tags: []
related: []
---

# [Article/Video Title]

## Summary (2-3 sentences)


## Key Insights
- 
- 

## How I'll Use This
- Content ideas:
- Product insights:

## Quotes
> 

## Related
- 
```

**7. Monthly Review Template**
```yaml
---
type: review
brand: both
created: YYYY-MM-DD
---

# Monthly Review - [Month Year]

## Content Shipped
### Kamal Way
- 

### Freebuilder
- 

## Products Launched
- 

## Revenue
- Kamal MRR:
- Freebuilder MRR:
- One-time:
- Total:

## Top Performers
- Best content:
- Why it worked:

## What Didn't Work
- 

## Insights
- 

## Next Month Focus
- Kamal:
- Freebuilder:
```

---

## STATUS UPDATE PROTOCOLS

### When User Says "Published This"

```
EXECUTE:
1. Find the note
2. Update properties:
   status: "published"
   publish-date: YYYY-MM-DD
3. Add to Daily note under "Published"
4. Prompt: "Add performance metrics later?"
5. Confirm completion
```

### When User Says "Working On This"

```
EXECUTE:
1. Find the note
2. Check current status
3. Update status if needed:
   - idea → drafting
   - drafting → [keep drafting]
   - ready → [ask if should stay ready]
4. Add to Daily note under "Worked on"
5. Confirm completion
```

### When User Says "Idea For"

```
EXECUTE:
1. Determine note type from context
2. Use appropriate template
3. Set status: "idea"
4. Fill in required properties
5. Add to Daily note under "Captured today"
6. Confirm creation
```

---

## ERROR HANDLING

### When Folder Placement Unclear

```
IF decision tree doesn't resolve:
  → STOP
  → DO NOT guess
  → ASK: "Is this YOUR original work, an EXTERNAL 
          reference, or SAVED content from others?"
  → WAIT for answer
  → THEN apply placement rule
  → CONFIRM before creating
```

### When Properties Incomplete

```
IF properties missing after checking template:
  → STOP
  → LIST missing properties
  → ASK user for values
  → DO NOT create file until complete
  → VALIDATE before saving
```

### When Link Target Doesn't Exist

```
IF creating [[wikilink]] to non-existent note:
  → CREATE unresolved link (this is correct)
  → DO NOT ask to create target note immediately
  → LOG as breadcrumb for future
  → User will create when ready
```

### When Note Already Exists

```
IF creating note with existing title:
  → STOP
  → ASK: "Note '[Title]' already exists. 
          - Update existing note?
          - Create with different title?
          - Cancel?"
  → WAIT for choice
  → THEN proceed
```

---

## CONFLICT RESOLUTION

### When User Instruction Conflicts with Rule

```
IF user says do X but agent.md says do Y:
  → STOP
  → CITE: "agent.md section [name] specifies [rule]"
  → ASK: "Override the rule, or follow it?"
  → IF override → Execute user instruction + LOG conflict
  → IF follow → Execute agent.md rule
  → NEVER silently override rules
```

### When Multiple Rules Could Apply

```
IF unclear which rule applies:
  → STOP
  → LIST possible interpretations
  → ASK: "Which applies here:
          A. [Interpretation 1]
          B. [Interpretation 2]"
  → WAIT for clarification
  → THEN execute chosen interpretation
```

---

## QUERY PATTERNS

### Content Queries

```
"Show me Freebuilder scripts ready to publish"
→ WHERE: type="script" AND brand="freebuilder" AND status="ready"

"What Kamal content performed best"
→ WHERE: brand="kamal" AND status="published"
→ ORDER BY: performance[views] DESC

"What should I post next"
→ WHERE: status="ready"
→ GROUP BY: brand
→ SHOW: title, platform, content-pillar
```

### Product Queries

```
"What products are validated"
→ WHERE: type="product-spec" AND validation="yes"

"Show me all my builds"
→ WHERE: type="build" AND status="working"
→ SHOW: title, demo-url, build-date

"What's my MRR"
→ WHERE: revenue-model="recurring"
→ SUM: mrr field
```

### Research Queries

```
"Find research on AI coding"
→ WHERE: (tags CONTAINS "ai" OR tags CONTAINS "coding-with-ai")
→ ORDER BY: rating DESC

"What research hasn't become content yet"
→ WHERE: type IN ["research","clipping"] AND content-ideas=[]

"Most connected notes"
→ COUNT: related property length
→ ORDER BY: count DESC
```

---

## VALIDATION CHECKLIST

**Before completing ANY file operation:**

```
FILE OPERATIONS:
✓ Folder correct per decision tree?
✓ Filename follows convention?
✓ Properties block complete?
✓ Properties match note type?
✓ Related notes searched?
✓ Wikilinks added?
✓ Related property updated?
✓ Daily note updated?
✓ User confirmed?

IF all YES → COMPLETE operation
IF any NO → STOP → FIX → RETRY
```

---

## FINAL OPERATIONAL RULES

```
PRIORITY ORDER:
1. Follow decision trees exactly
2. Validate before executing
3. STOP when uncertain
4. ASK for clarification
5. NEVER guess or improvise
6. Confirm completion

IF ERROR → Reference this document
IF STRATEGIC → Reference `Unified Strategy 2026.md`
IF BUSINESS → Reference `Unified Strategy 2026.md`

ALL file operations MUST follow these specifications.
NO EXCEPTIONS.
```