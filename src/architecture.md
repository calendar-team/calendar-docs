# Architecture overview

Currently, the *calendar* project has 3 components:
- [calendar-frontend](./calendar-frontend.md): the frontend written using Next.js
- [calendar-backend](./calendar-backend.md): the backend written in Rust
- `calendar-docs`: this book

```mermaid
flowchart TD
  subgraph browser["fab:fa-internet-explorer Browser"]
    direction TB
    calendar-frontend-client-side("Client side of calendar-frontend")
  end

  subgraph vercel["fab:fa-server Vercel"]
    calendar-frontend-server-side("Server side of calendar-frontend")
  end

  subgraph ec2["fab:fa-server EC2"]
    direction TB
    calendar-backend --> sqlite
  end

  client("fal:fa-user Client")
  sqlite("fab:fa-database SQLite")
  calendar-backend(calendar-backend)

  client -- "<a href='https://calendar-frontend-ten.vercel.app/' target='_blank'>calendar-frontend-ten.vercel.app</a>" --> browser
  browser --> vercel --> ec2
  browser --> ec2
```
