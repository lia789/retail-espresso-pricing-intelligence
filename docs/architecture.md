# Initial Architecture

## Goal
```
Build a simple daily pricing pipeline that runs completely on a local development machine.
```


## High-Level Flow

```
Local CLI Command
    ↓
Source Adapter
    ↓
Fetcher
    ↓
Parser
    ↓
Normalize + Validate
    ↓
Change Detection
    ↓
SQLite Database
    ↓
Crawl Summary
```

## Initial Decisions
```
- Run entirely on the local development machine.
- Use a Python CLI application.
- Use SQLite for the first version.
- Store the SQLite database locally.
- Keep each retailer in a separate source adapter.
```

## Later Improvements
```
Possible future upgrades:
- PostgreSQL
- Docker
- automated scheduling
- concurrency and retries
- monitoring and structured logging
- production deployment
```