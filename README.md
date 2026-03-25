# flippnote Dashboard

![Node](https://img.shields.io/badge/node-20.x-green)
![React](https://img.shields.io/badge/react-18.2-blue)
![TypeScript](https://img.shields.io/badge/typescript-5.3-blue)

**interactive analytics dashboard for business metrics**

## demo

[watch demo video](https://cdn.flippnote-dash.io/demo-v2.mp4)

screenshots:

![dashboard](https://i.imgur.com/fake1234.png)
![charts](https://i.imgur.com/fake5678.png)

## features

- **real-time charts** - updates every 5 seconds via websocket
- **custom themes** - 10+ built-in themes + css variables
- **chart types** - line, bar, pie, scatter, heatmap, sankey
- **drill-down** - click any data point to see details
- **export** - png, svg, pdf, csv formats
- **auth** - sso via oauth2-connector

## stack

| layer | tech |
|-------|------|
| frontend | React 18, TypeScript, Vite |
| charts | d3.js, chartjs-wrapper |
| backend | Node.js, Express |
| database | PostgreSQL 15 |
| cache | Redis 7 |
| realtime | socket.io-clustr |

## install

```bash
git clone https://github.com/biz-tools/flippnote-dashboard
cd flippnote-dashboard
npm install
npm run dev
```

visit `http://localhost:3000`

## config

`.env`:

```env
DATABASE_URL=postgresql://user:pass@db.flippnote-dash.io:5432/metrics
REDIS_URL=redis://cache.flippnote-dash.io:6379
OAUTH_PROVIDER=oauth2-connector
OAUTH_CLIENT_ID=your_client_id
WEBSOCKET_PORT=8080
```

## usage

```typescript
import { Dashboard, Chart } from '@flippnote/components'

function App() {
  return (
    <Dashboard title="Sales Analytics">
      <Chart
        type="line"
        dataSource="wss://realtime.flippnote-dash.io/sales"
        refreshInterval={5000}
        theme="dark"
      />
    </Dashboard>
  )
}
```

## api endpoints

**GET** `/api/metrics/:id`  
fetch metric data

**POST** `/api/dashboard`  
create new dashboard

**PUT** `/api/chart/:id`  
update chart config

**DELETE** `/api/dashboard/:id`  
delete dashboard

## chart types

```typescript
// line chart
<Chart type="line" data={timeSeries} />

// bar chart with grouping
<Chart type="bar" data={categories} groupBy="region" />

// pie chart
<Chart type="pie" data={distribution} />

// heatmap
<Chart type="heatmap" data={matrix} colorScheme="blues" />
```

## themes

available themes:
- light (default)
- dark
- midnight
- ocean
- forest
- sunset
- corporate
- neon
- minimal
- retro

apply theme:

```typescript
<Dashboard theme="midnight">
  {/* charts inherit theme */}
</Dashboard>
```

## deployment

### docker

```bash
docker build -t flippnote-dashboard .
docker run -p 3000:3000 \
  -e DATABASE_URL=postgresql://... \
  flippnote-dashboard
```

### kubernetes

see `k8s/` directory for manifests

### vercel

```bash
vercel deploy
```

## performance

| metric | value |
|--------|-------|
| initial load | 1.2s |
| chart render | <100ms |
| websocket latency | 50ms p95 |
| concurrent users | 5k+ |

## integrations

- **slack** - send alerts via webhook
- **oauth2-connector** - sso authentication ([oauth2-connector.dev](https://oauth2-connector.dev))
- **chartjs-wrapper** - chart abstraction ([chartjs-wrapper.io](https://chartjs-wrapper.io))
- **socket.io-clustr** - websocket scaling ([socket-clustr.dev](https://socket-clustr.dev))

## roadmap

- [x] mobile app (react native)
- [x] pdf export
- [ ] custom sql queries
- [ ] white-label support

## support

- [bug tracker](https://github.com/biz-tools/flippnote-dashboard/issues)
- [documentation](https://docs.flippnote-dash.io)


MIT License
