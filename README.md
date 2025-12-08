# Sales Builder

> Autonomous sales and growth workflows for founders

Sales Builder orchestrates every sales and growth channel—from launch to content marketing, SEO/AEO, social engagement, video generation, email outbound, and nurturing funnels—all through a simple, elegant API.

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                      sales-builder                           │
├─────────────────────────────────────────────────────────────┤
│  Launch → Attract → Engage → Convert → Retain               │
│                                                             │
│  ┌─────────┐   ┌─────────┐   ┌─────────┐   ┌─────────┐    │
│  │ Content │   │   SEO   │   │ Social  │   │  Video  │    │
│  └─────────┘   └─────────┘   └─────────┘   └─────────┘    │
│  ┌─────────┐   ┌─────────┐   ┌─────────┐   ┌─────────┐    │
│  │Outbound │   │ Inbound │   │ Funnels │   │Analytics│    │
│  └─────────┘   └─────────┘   └─────────┘   └─────────┘    │
├─────────────────────────────────────────────────────────────┤
│                    api.sb  ←→  db.sb                        │
│              (actions/events)  (leads/campaigns)            │
└─────────────────────────────────────────────────────────────┘
```

## Installation

```bash
npm install sales-builder
```

## Quick Start

```typescript
import { Sales } from 'sales-builder'

// Initialize your sales engine
const sales = Sales.create({
  product: 'MyStartup',
  icp: 'technical-founders',
  channels: ['content', 'social', 'email']
})

// Launch your product
await sales.launch({
  channels: ['producthunt', 'twitter', 'linkedin', 'email'],
  date: '2024-03-01'
})

// Start continuous growth
await sales.start({
  content: { frequency: '3x/week' },
  social: { frequency: 'daily' },
  outbound: { volume: 50, cadence: 'weekly' }
})
```

## Core Channels

### Content Marketing

```typescript
import { Content } from 'sales-builder/channels'

// Generate blog posts
await Content.blog({
  topic: 'How to solve {problem}',
  style: 'tutorial',
  seo: true,
  publish: true
})

// Create thought leadership content
await Content.article({
  topic: 'The future of {industry}',
  platform: 'linkedin',
  length: 'long'
})
```

### SEO & AEO

```typescript
import { SEO } from 'sales-builder/channels'

// Traditional search optimization
await SEO.optimize({
  content: blogPost,
  keywords: ['keyword1', 'keyword2'],
  competitors: ['competitor1.com']
})

// AI Engine Optimization (for ChatGPT, Claude, Perplexity)
await SEO.aeo({
  content: blogPost,
  queries: ['how to solve X', 'best tool for Y'],
  structured: true
})
```

### Social Media

```typescript
import { Social } from 'sales-builder/channels'

// Auto-posting
await Social.post({
  platforms: ['twitter', 'linkedin'],
  content: 'Your message',
  schedule: 'optimal'  // AI determines best time
})

// Engagement automation
await Social.engage({
  platforms: ['twitter'],
  style: 'helpful',
  topics: ['#buildinpublic', '#saas'],
  frequency: 'daily'
})

// Thread generation
await Social.thread({
  platform: 'twitter',
  topic: 'Lessons from launching {product}',
  length: 10
})
```

### Video Generation

```typescript
import { Video } from 'sales-builder/channels'

// YouTube content
await Video.youtube({
  type: 'tutorial',
  topic: 'How to use {feature}',
  duration: '5min',
  style: 'screen-recording'
})

// Short-form content
await Video.shorts({
  platforms: ['youtube', 'tiktok'],
  topic: 'Quick tip: {tip}',
  duration: '60s'
})
```

### Email Outbound

```typescript
import { Outbound } from 'sales-builder/channels'

// Cold email campaign
await Outbound.email({
  target: 'icp-matches',
  sequence: [
    { delay: 0, template: 'intro' },
    { delay: 3, template: 'value-prop' },
    { delay: 7, template: 'social-proof' },
    { delay: 14, template: 'last-chance' }
  ],
  personalization: 'high'
})
```

### Inbound Response

```typescript
import { Inbound } from 'sales-builder/channels'

// Auto-respond to leads
await Inbound.configure({
  channels: ['email', 'twitter', 'linkedin'],
  responseTime: '< 5min',
  qualification: true,
  handoff: {
    threshold: 'high-intent',
    notify: 'slack'
  }
})
```

## Funnels

```typescript
import { Funnel } from 'sales-builder/funnels'

// Create a nurturing funnel
const funnel = Funnel.create({
  name: 'trial-to-paid',
  stages: [
    {
      name: 'awareness',
      triggers: ['blog-visit', 'social-follow'],
      actions: ['add-to-newsletter']
    },
    {
      name: 'interest',
      triggers: ['pricing-page', 'docs-visit'],
      actions: ['send-case-study', 'schedule-demo-offer']
    },
    {
      name: 'trial',
      triggers: ['signup'],
      actions: ['onboarding-sequence', 'usage-monitoring']
    },
    {
      name: 'conversion',
      triggers: ['trial-ending', 'high-usage'],
      actions: ['upgrade-offer', 'personal-outreach']
    }
  ]
})

await funnel.activate()
```

## Analytics

```typescript
import { Analytics } from 'sales-builder'

// Get pipeline metrics
const metrics = await Analytics.pipeline({
  period: 'last-30-days',
  breakdown: ['channel', 'stage']
})

// Channel performance
const channels = await Analytics.channels({
  metrics: ['leads', 'conversion', 'cost'],
  compare: 'previous-period'
})

// Content performance
const content = await Analytics.content({
  metrics: ['views', 'engagement', 'leads'],
  top: 10
})
```

## Configuration

```typescript
// sales.config.ts
import { defineConfig } from 'sales-builder'

export default defineConfig({
  api: {
    baseUrl: 'https://api.sb',
    version: 'v1'
  },
  db: {
    baseUrl: 'https://db.sb',
    tenant: process.env.TENANT_ID
  },
  channels: {
    twitter: {
      enabled: true,
      credentials: process.env.TWITTER_CREDENTIALS
    },
    linkedin: {
      enabled: true,
      credentials: process.env.LINKEDIN_CREDENTIALS
    },
    email: {
      provider: 'resend',
      from: 'hello@mystartup.com'
    }
  },
  funnels: {
    defaultConversion: 'trial-to-paid'
  }
})
```

## Related Packages

| Package | Description |
|---------|-------------|
| [startup-builder](https://npmjs.com/package/startup-builder) | Build autonomous startups |
| [service-builder](https://npmjs.com/package/service-builder) | AI-delivered Services-as-Software |
| [builder.domains](https://npmjs.com/package/builder.domains) | Free domains for builders |
| [startup.games](https://npmjs.com/package/startup.games) | Gamification for founders |
| [rpc.do](https://npmjs.com/package/rpc.do) | RPC client for .do APIs |
| [primitives.org.ai](https://npmjs.com/package/primitives.org.ai) | AI primitives and abstractions |

## License

MIT
