# 🌍 OmniIndex
### A Distributed Personal Metadata Search Engine

OmniIndex is a cross-platform, distributed metadata indexing system that allows users to search and locate their files across multiple devices and storage platforms from a single unified interface.

It does **not store actual files**.  
It stores **file metadata only**, enabling fast, privacy-focused global search across devices.

---

# 🚀 Vision

Modern operating systems provide local indexing:
- Windows Search
- macOS Spotlight
- Linux tracker/locate

Cloud platforms provide search inside their own ecosystem:
- Google Drive
- Dropbox
- OneDrive

But there is no unified, cross-device, cross-platform personal search layer.

OmniIndex aims to become:

> A Personal Distributed Metadata Engine  
> That lets users instantly locate where any file exists across all their devices.

Example search result:


File: asdf.mkv

Device: Redmi 9 Pro
Path: /media/video/asdf.mkv

Device: Ubuntu Laptop
Path: /home/adhnan/movies/asdf.mkv

Drive: adhna...@example.com

Path: me/kfkf/png


---

# 🧠 Core Concept

OmniIndex does NOT:

- Copy files
- Backup files
- Store binary content

OmniIndex DOES:

- Index file metadata
- Track file locations
- Sync metadata to cloud
- Provide unified search
- Work offline-first

---

# 🏗 Architecture Overview

The system consists of three major layers:

## 1️⃣ Device Agent Layer (Open Core)

Each device runs a lightweight background agent.

Responsibilities:
- Watch filesystem changes
- Store local metadata (SQLite)
- Track file events (create/update/delete)
- Sync metadata with cloud when online

First implementation target:
- Ubuntu Linux

Future:
- Windows
- macOS
- Android
- iOS

---

## 2️⃣ Sync Protocol Layer

All communication between devices and cloud happens through a stable, versioned API contract.

Example:

```json
POST /sync

{
  "deviceId": "uuid",
  "lastSyncVersion": 124,
  "changes": [...]
}
```

Key principles:

Delta-based sync

Versioned updates

Event-based tracking

Conflict-aware design

Offline-first architecture

3️⃣ Cloud Core (SaaS Backend)

The cloud is the control center.

Responsibilities:

User authentication

Device registration

Metadata storage

Sync processing

Unified search

Multi-device management

Tech stack (planned):

Node.js

PostgreSQL

Redis (caching)

Docker

JWT-based authentication

📦 What We Store

We store metadata only.

Example:

{
  "file_id": "uuid",
  "device_id": "uuid",
  "user_id": "uuid",
  "file_name": "report.pdf",
  "full_path": "/home/user/docs/report.pdf",
  "extension": "pdf",
  "size": 204800,
  "hash": "sha256...",
  "created_at": "...",
  "modified_at": "...",
  "indexed_at": "...",
  "is_deleted": false
}

We do NOT store:

File binary data

File contents (Phase 1)

User file uploads

🔄 Sync Model

OmniIndex uses an Eventual Consistency Model.

Each device:

Maintains a local metadata database

Tracks changes as events

Pushes deltas when online

Pulls sync state updates

Cloud:

Maintains global metadata state

Tracks device versions

Merges metadata safely

Deletion tracking:

Soft deletes only

No hard deletion

Versioned state changes

🧱 Core Database Structure (Cloud)

Tables:

users
devices
files
file_events
sync_state

All entities use UUIDs.

No auto-increment IDs.

🔐 Security Design

JWT authentication

Device-level authorization

Per-user isolation

Metadata-only storage (privacy-first)

HTTPS-only API

Future:

End-to-end metadata encryption

Zero-knowledge architecture

🌐 Open Core Strategy

OmniIndex follows an Open Core + SaaS model.

Open Source:

Device agent

Sync client

Basic self-host server

Protocol documentation

SaaS Cloud:

Managed hosting

Global unified search

Multi-device dashboard

Advanced indexing

Performance optimizations

AI-powered search (future)

🧩 Phase Roadmap
Phase 1 – Core MVP

Cloud backend

Auth system

Device registration

Metadata storage

Ubuntu agent

Basic filename search

Phase 2 – Sync Improvements

Delta optimization

Hash comparison

Deletion tracking

Redis caching

Phase 3 – Multi-Platform

Windows agent

macOS agent

Web dashboard

Phase 4 – Advanced Search

Full-text indexing

Ranking algorithms

Device-based filtering

AI semantic search

🎯 Why This Matters

OmniIndex is not just a search tool.

It demonstrates:

Distributed systems thinking

Offline-first architecture

Sync engine design

SaaS multi-tenant systems

Cross-platform engineering

Event-driven metadata modeling

This project is designed to evolve from:
Developer tool → Power user utility → SaaS platform

📌 Design Principles

Core logic lives in cloud

Device agents remain thin

Metadata only, never file content (Phase 1)

Offline-first

Versioned sync

UUID-based identity

Soft deletes only

API-first architecture

🧠 Long-Term Vision

OmniIndex can evolve into:

Personal digital life index

Knowledge engine

Developer productivity tool

Enterprise metadata search layer

Privacy-first alternative to centralized ecosystems

🛠 Initial Target Platform

Ubuntu Linux device agent.

This will validate:

Filesystem watching

Local metadata storage

Sync protocol

Core SaaS functionality

Once stable, expansion to other platforms will reuse the same protocol layer.
