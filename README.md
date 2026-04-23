# ServisBot Fullstack Code Challenge

Welcome, and thank you for taking the time to work on this challenge! This is a chance to showcase your fullstack abilities across API design, data handling, and UI/UX.
Feel free to fork this repo, or create your own repo and complete the task.

## Overview

You'll build a small fullstack application that exposes a dataset of **bots**, **workers**, and **logs** through a REST API, and a UI that lets users explore the relationships between them.

A few ground rules:

- Use whatever technologies you prefer. NodeJS and ExpressJS (or similar) on the backend are common choices - pick what lets you do your best work.
- Handle the provided data in a way that is efficient and fits the requirements below.
- This does **not** need to be production-ready. Show us how you think — comments and notes about trade-offs are very welcome.


## Some things we like

There's no single right answer, and we're deliberately not going to prescribe *how* you build this. That said, some of the considerations we look for are laid out below. How you choose to address them is up to you:

- **Correctness** - the application does what's asked and handles any edge cases.
- **Separation of concerns** — the boundaries between API, domain logic, data access, and UI are visible and deliberate, not accidental.
- **Simplicity / restraint** — the solution is no more complex than the problem demands. Abstractions earn their keep; scaffolding doesn't outweigh the feature set.
- **API design** — resource shapes, URLs, and status codes feel considered. Thought has been given to what the UI actually needs.
- **Product sense / UX** — empty states, loading, navigation, and clear interactions suggest the candidate thought about the user, not just the code.
- **Performance awareness** — efficient handling of the larger data, especially where the API hands off to the UI.
- **Communication** — the README, commit history, and inline notes make it easy for a reviewer to follow the thinking.
- **Consistency** — naming, patterns, and conventions hold up across the codebase.

We're more interested in the thinking behind your trade-offs than in any particular framework, pattern, or tool.

## Getting Started

Sample data lives in the [data/](data/) directory as JSON files you can load directly into your application:

- [data/bots.json](data/bots.json)
- [data/workers.json](data/workers.json)
- [data/logs.json](data/logs.json)

Take some time to familiarize yourself with the data — its shape and scale may influence your design choices significantly.

If you want to regenerate the sample data:

```sh
npm install
npm start
```

## Data Models

### Bot

```jsonc
{
  "id": "04140c19-0c46-43c6-8e78-f459cd3b3370",  // Immutable, Required, UUID
  "name": "Bot One",                              // Mutable,   Required, String
  "description": "First Bot",                     // Mutable,   Optional, String
  "status": "DISABLED",                           // Mutable,   Required, Enum: "DISABLED" | "ENABLED" | "PAUSED"
  "created": 1713809849892                        // Immutable, Required, Epoch ms
}
```

### Worker

```jsonc
{
  "id": "6f4fdfd9-da33-4711-9386-579e8101dc43",  // Immutable, Required, UUID
  "name": "Worker One",                           // Mutable,   Required, String
  "description": "First Worker",                  // Mutable,   Optional, String
  "bot": "Bot One",                               // Mutable,   Required, references a Bot
  "created": 1713773401591                        // Immutable, Required, Epoch ms
}
```

### Log

```jsonc
{
  "id": "a3922ad6-49ed-4cf3-8293-cc4d58a5d4c9",    // Immutable, Required, UUID
  "created": "2024-04-22T14:14:14.926Z",           // Immutable, Required, ISO timestamp
  "message": "Some Message",                       // Mutable,   Required, String
  "bot": "44700aa2-cba6-43d2-9ad4-8d8a499bd356",   // Immutable, Required, references a Bot (UUID)
  "worker": "e5d7874c-fd2d-41b8-abc1-2e311964ae8c" // Immutable, Required, references a Worker (UUID)
}
```

### Relationships

- **Bot** → **Workers** (1:M)
- **Bot** → **Logs** (1:M)
- **Worker** → **Logs** (1:M)

## The Challenge

Build an application that supports the following features:

- View the list of bots
- View the list of workers for a bot
- View the list of logs for a bot
- View the list of logs for a worker associated with a bot

### API

Expose these features via a RESTful API with read endpoints returning the data in shapes that make sense for the UI.

### UI

There are no wireframes or design specifications. Apply a UI/UX that delivers an intuitive experience for the feature set above — make it your own.
