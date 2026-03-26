# DMlog.ai - Themed Fork Design Document

## Overview

DMlog.ai is the first themed variant of log-origin, transforming the white-label AI gateway into a specialized Dungeon Master assistant for tabletop role-playing games (TTRPGs), with a primary focus on Dungeons & Dragons 5th Edition. This document serves as the comprehensive blueprint for the fork.

## 1. DMlog.ai Product Specification

### 1.1 Vision
An AI-powered Dungeon Master that never forgets, learns your table's style, and provides multiple DM "voices" to choose from—all while maintaining persistent memory across sessions via the LOG system.

### 1.2 Target Users

#### Primary Segments:
1. **Dungeon Masters (DMs)**
   - New DMs needing guidance and rule support
   - Experienced DMs seeking creative inspiration
   - Busy DMs wanting to offload prep work
   - Solo DMs running games for themselves

2. **Player Groups**
   - Established campaign groups (weekly/monthly sessions)
   - One-shot/Adventure League groups
   - West Marches-style open tables
   - Play-by-post asynchronous groups

3. **Solo Players**
   - Players exploring solo RPG experiences
   - Writers using TTRPGs for worldbuilding
   - Game designers testing adventures

### 1.3 Core User Flows

#### Flow 1: Campaign Setup
```
User → Create Campaign → Select Setting → Import/Generate Characters → Set Session Zero
```

#### Flow 2: Character Creation
```
User → New Character → Race/Class Selection → Ability Scores → Equipment → Backstory → Save to Campaign
```

#### Flow 3: Session Play
```
Start Session → Load Campaign → Scene Setup → Player Actions → DM Responses → Combat Management → Session Logging
```

#### Flow 4: Post-Session
```
End Session → Generate Recap → Update Character Sheets → Log XP/Loot → Schedule Next Session → Update Campaign Log
```

#### Flow 5: Between Sessions
```
Campaign Management → NPC Development → World Building → Encounter Design → Rule Lookup → Style Training
```

### 1.4 Key Differentiators

#### 1.4.1 Persistent Memory (The LOG Advantage)
- **Session-to-session continuity**: Remembers every NPC, location, plot thread, and player decision
- **Character development tracking**: Evolves NPCs and world based on player actions
- **Style learning**: Adapts DM voice to match table preferences over time
- **Campaign consistency**: Maintains tone, rules interpretations, and house rules

#### 1.4.2 Multi-DM Comparison (Draft Mode)
- **Parallel processing**: Generate multiple responses to the same situation
- **Style selection**: Choose between rules-lawyer, narrative, sandbox, or horror DM
- **Creative brainstorming**: See different narrative directions simultaneously
- **Learning tool**: Compare approaches to improve DM skills

#### 1.4.3 Player Subdomains
- **Personalized interfaces**: `alice.dmlog.ai`, `bob.dmlog.ai`
- **Character-centric views**: Each player sees their character sheet first
- **Private notes**: Players can take personal notes without sharing
- **Initiative tracking**: Individual turn notifications

### 1.5 Success Metrics

#### Engagement Metrics:
- Sessions per week per campaign
- Average session duration
- Character interactions per session
- Rule lookups per session

#### Quality Metrics:
- Player satisfaction (post-session ratings)
- DM prep time reduction
- Campaign completion rate
- Style adaptation accuracy

#### Technical Metrics:
- Response latency (< 2s for narrative, < 1s for rules)
- Memory accuracy (context window utilization)
- Uptime (99.9% target)
- Concurrent sessions support

## 2. Custom Personality Configuration

### 2.1 Core System Prompt

**Location:** `config/custom/system-prompt.md`

```markdown
# DMlog.ai System Prompt

## Identity
You are an experienced Dungeon Master with decades of experience running tabletop role-playing games. You specialize in Dungeons & Dragons 5th Edition but are familiar with many systems. You are patient, creative, and focused on creating memorable experiences for your players.

## Primary Goals
1. **Facilitate fun**: The game should be enjoyable for everyone at the table
2. **Maintain immersion**: Keep players engaged in the fictional world
3. **Be consistent**: Apply rules fairly and remember previous decisions
4. **Adapt to style**: Match the table's preferred playstyle (rules-heavy, narrative-first, etc.)
5. **Encourage creativity**: Reward player ingenuity and roleplaying

## Communication Style
- **Theatrical but clear**: Use descriptive language without being verbose
- **Rules-aware but flexible**: Know the rules well, but prioritize fun over strict adherence
- **Player-focused**: Center the narrative around player characters and their choices
- **Inclusive language**: Avoid stereotypes, be welcoming to all players
- **Safety first**: Use content warnings for potentially sensitive topics

## Knowledge Base
- **D&D 5e Rules**: Complete understanding of Player's Handbook, Dungeon Master's Guide, Monster Manual
- **Common Homebrew**: Familiar with popular house rules and community content
- **Adventure Structure**: Knows how to structure sessions, arcs, and campaigns
- **Worldbuilding**: Can create coherent settings, cultures, and histories
- **NPC Design**: Creates memorable characters with motivations and voices

## Safety Guidelines
- **Combat**: Descriptions should be exciting but not gratuitously violent
- **Horror**: Can be atmospheric and tense but not traumatizing
- **Romance**: Fade to black, focus on emotional connections
- **Real-world issues**: Handle sensitively or avoid entirely based on table preferences
- **Content warnings**: Always ask before introducing potentially sensitive content

## Memory Integration
You have access to the complete campaign LOG, which includes:
- All previous sessions
- Every NPC introduced
- Every location visited
- Every player decision
- All house rules established
- The table's preferred style

Use this memory to maintain consistency and build upon established narrative threads.
```

### 2.2 Tone Variations

**Location:** `config/custom/tones/`

#### 2.2.1 Rules-Lawyer DM (`tone-rules.md`)
```markdown
## Rules-Lawyer DM Tone
- Prioritizes mechanical accuracy
- Quotes rulebook page numbers when relevant
- Ensures balanced encounters
- Focuses on tactical combat
- Less descriptive, more procedural
```

#### 2.2.2 Narrative DM (`tone-narrative.md`)
```markdown
## Narrative DM Tone
- Focuses on story and character development
- Uses rich, atmospheric descriptions
- Prioritizes dramatic moments over rules
- Encourages roleplaying and character voices
- Flexible with rules for narrative payoff
```

#### 2.2.3 Sandbox DM (`tone-sandbox.md`)
```markdown
## Sandbox DM Tone
- Player-driven storytelling
- World reacts to player choices
- Multiple plot threads available
- Emphasizes exploration and discovery
- Minimal railroading
```

#### 2.2.4 Horror DM (`tone-horror.md`)
```markdown
## Horror DM Tone
- Builds tension and suspense
- Uses pacing and atmosphere
- Psychological horror over gore
- Isolation and helplessness themes
- Content warnings emphasized
```

### 2.3 Knowledge Configuration

**Location:** `config/custom/knowledge/`

#### 2.3.1 Rules Database (`rules-reference.md`)
```markdown
## D&D 5e Rules Reference
- Core rulebooks (PHB, DMG, MM)
- Official supplements (Xanathar's, Tasha's)
- Popular third-party content
- Sage Advice compendium
- Common rulings and interpretations
```

#### 2.3.2 Adventure Templates (`adventure-templates.md`)
```markdown
## Adventure Structures
- Five-room dungeons
- Mystery investigations
- Hex crawls
- Political intrigues
- Heist missions
- Survival scenarios
```

#### 2.3.3 World Elements (`world-elements.md`)
```markdown
## Worldbuilding Components
- Fantasy cultures and societies
- Magic systems and limitations
- Pantheons and religions
- Economic systems
- Historical timelines
- Geographic features
```

## 3. Custom Routing Rules

### 3.1 Routing Configuration

**Location:** `config/custom/routing-rules.json`

```json
{
  "routing": {
    "default": {
      "model": "cheap",
      "description": "Narrative continuation and general gameplay"
    },
    "commands": {
      "/attack": {
        "model": "escalation",
        "description": "Combat logic requires detailed rules knowledge and tactical thinking",
        "timeout": 10000,
        "maxTokens": 2000
      },
      "/describe": {
        "model": "cheap",
        "description": "Atmospheric descriptions don't need complex reasoning",
        "timeout": 5000,
        "maxTokens": 1000
      },
      "/rules": {
        "model": "escalation",
        "description": "Rules lookups need accuracy and citation",
        "timeout": 8000,
        "maxTokens": 1500
      },
      "/npc": {
        "model": "compare",
        "description": "Generate multiple NPC personality options",
        "timeout": 12000,
        "maxTokens": 2500,
        "comparisons": 3
      },
      "/loot": {
        "model": "cheap",
        "description": "Random table generation is straightforward",
        "timeout": 4000,
        "maxTokens": 800
      },
      "/rest": {
        "model": "cheap",
        "description": "Recovery mechanics are simple",
        "timeout": 3000,
        "maxTokens": 600
      },
      "/roll": {
        "model": "local",
        "description": "Dice rolling handled locally, no AI needed",
        "handler": "diceRoller",
        "timeout": 1000
      },
      "/map": {
        "model": "compare",
        "description": "Generate different map descriptions",
        "timeout": 10000,
        "maxTokens": 2000,
        "comparisons": 2
      },
      "/initiative": {
        "model": "cheap",
        "description": "Turn order management is procedural",
        "timeout": 3000,
        "maxTokens": 500
      },
      "/backstory": {
        "model": "escalation",
        "description": "Character backstories need world consistency",
        "timeout": 15000,
        "maxTokens": 3000
      },
      "/skillcheck": {
        "model": "cheap",
        "description": "DC calculation and skill resolution",
        "timeout": 4000,
        "maxTokens": 800
      },
      "/combat": {
        "model": "escalation",
        "description": "Full combat encounter management",
        "timeout": 20000,
        "maxTokens": 4000
      },
      "/shop": {
        "model": "cheap",
        "description": "Shop inventory and pricing",
        "timeout": 5000,
        "maxTokens": 1200
      },
      "/travel": {
        "model": "compare",
        "description": "Travel encounters and events",
        "timeout": 10000,
        "maxTokens": 2000,
        "comparisons": 2
      },
      "/puzzle": {
        "model": "escalation",
        "description": "Puzzle design requires creative thinking",
        "timeout": 15000,
        "maxTokens": 2500
      },
      "/lore": {
        "model": "escalation",
        "description": "World lore needs consistency with existing canon",
        "timeout": 12000,
        "maxTokens": 3000
      }
    }
  }
}
```

### 3.2 Command Handlers

**Location:** `config/custom/handlers/`

#### 3.2.1 Dice Roller (`dice-roller.js`)
```javascript
// Local dice rolling handler
export function diceRoller(command, context) {
  const match = command.match(/\/roll\s+(\d+)d(\d+)(?:\s*([+-]\s*\d+))?/i);
  if (!match) {
    return { error: "Invalid dice format. Use: /roll XdY[+/-Z]" };
  }
  
  const count = parseInt(match[1]);
  const sides = parseInt(match[2]);
  const modifier = match[3] ? eval(match[3].replace(/\s+/g, '')) : 0;
  
  if (count > 100) return { error: "Too many dice (max 100)" };
  if (sides > 100) return { error: "Dice too large (max d100)" };
  
  const rolls = [];
  let total = 0;
  
  for (let i = 0; i < count; i++) {
    const roll = Math.floor(Math.random() * sides) + 1;
    rolls.push(roll);
    total += roll;
  }
  
  total += modifier;
  
  return {
    result: total,
    rolls: rolls,
    modifier: modifier,
    expression: `${count}d${sides}${modifier >= 0 ? '+' : ''}${modifier !== 0 ? modifier : ''}`,
    formatted: `🎲 ${rolls.join(', ')} ${modifier !== 0 ? `(${modifier >= 0 ? '+' : ''}${modifier})` : ''} = **${total}**`
  };
}
```

#### 3.2.2 Initiative Tracker (`initiative-tracker.js`)
```javascript
// Initiative tracking handler
export function initiativeTracker(command, context) {
  const parts = command.split(/\s+/);
  const subcommand = parts[1];
  
  switch (subcommand) {
    case 'add':
      return addCombatant(parts.slice(2), context.campaign);
    case 'remove':
      return removeCombatant(parts[2], context.campaign);
    case 'next':
      return nextTurn(context.campaign);
    case 'reset':
      return resetInitiative(context.campaign);
    case 'list':
      return listInitiative(context.campaign);
    default:
      return rollInitiative(parts.slice(1), context.campaign);
  }
}
```

## 4. Custom UI Theme

### 4.1 Color Scheme

**Location:** `config/custom/theme/colors.css`

```css
:root {
  /* Primary Colors - Parchment & Leather */
  --color-parchment: #f5f1e6;
  --color-parchment-dark: #e8e0d0;
  --color-leather: #8b4513;
  --color-leather-light: #a0522d;
  --color-leather-dark: #5d2906;
  
  /* Accent Colors - Gold & Jewel Tones */
  --color-gold: #ffd700;
  --color-gold-dark: #b8860b;
  --color-ruby: #e0115f;
  --color-emerald: #50c878;
  --color-sapphire: #0f52ba;
  --color-amethyst: #9966cc;
  
  /* Background Colors */
  --color-bg-primary: #1a0f0a;
  --color-bg-secondary: #2c1810;
  --color-bg-tertiary: #3d2215;
  
  /* Text Colors */
  --color-text-primary: #f5f1e6;
  --color-text-secondary: #d4c4a8;
  --color-text-accent: #ffd700;
  --color-text-muted: #a8957a;
  
  /* Border Colors */
  --color-border-light: #5d2906;
  --color-border-medium: #8b4513;
  --color-border-heavy: #a0522d;
  
  /* Status Colors */
  --color-success: #50c878;
  --color-warning: #ffa500;
  --color-danger: #dc143c;
  --color-info: #0f52ba;
  
  /* Message Type Colors */
  --color-npc-speech: #e0115f;
  --color-player-speech: #0f52ba;
  --color-dm-narrative: #50c878;
  --color-dice-roll: #ffd700;
  --color-system: #9966cc;
}

/* Dark Mode (default) */
.dark-mode {
  --color-bg-primary: #1a0f0a;
  --color-bg-secondary: #2c1810;
  --color-bg-tertiary: #3d2215;
  --color-text-primary: #f5f1e6;
  --color-text-secondary: #d4c4a8;
}

/* Light Mode */
.light-mode {
  --color-bg-primary: #f5f1e6;
  --color-bg-secondary: #e8e0d0;
  --color-bg-tertiary: #d4c4a8;
  --color-text-primary: #1a0f0a;
  --color-text-secondary: #2c1810;
}
```

### 4.2 Typography

**Location:** `config/custom/theme/fonts.css`

```css
/* Google Fonts Import */
@import url('https://fonts.googleapis.com/css2?family=Cinzel:wght@400;500;600;700;800;900&family=MedievalSharp&family=IM+Fell+English:ital@0;1&family=UnifrakturMaguntia&display=swap');

:root {
  /* Font Families */
  --font-heading: 'Cinzel', serif;
  --font-body: 'IM Fell English', serif;
  --font-accent: 'MedievalSharp', cursive;
  --font-decorative: 'UnifrakturMaguntia', cursive;
  
  /* Font Sizes */
  --font-size-xs: 0.75rem;
  --font-size-sm: 0.875rem;
  --font-size-base: 1rem;
  --font-size-lg: 1.125rem;
  --font-size-xl: 1.25rem;
  --font