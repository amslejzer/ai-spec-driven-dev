# Specification Example

**Method version:** 1.1

## Summary

- Problem: Reading status is currently tracked inconsistently
- Audience: A solo user
- Success criteria: The user can create, update, and review book entries without using scattered notes

## Scope

- In scope: add books, update reading status, store optional notes, view current and finished books
- Out of scope: accounts, sharing, recommendations, import/export

## System Overview

- Major components: entry management, list views, local persistence
- Responsibilities: store simple reading records and expose basic status-based views
- Boundaries: single-user local-first app

## Key Flows

### Add Book

- Trigger: user decides to track a book
- Steps: enter title, optional author, initial status, optional note
- Expected outcome: a new reading entry is saved and visible in the appropriate list

### Update Status

- Trigger: user starts or finishes a book
- Steps: change status and set the relevant date
- Expected outcome: the entry appears in the correct filtered list

## Data and State

- Important entities: book entry, status, notes, started date, finished date
- State transitions: to-read -> reading -> finished
- Persistence needs: save entries locally between sessions

## Constraints

- Technical constraints: keep the first version simple and local-first
- Product constraints: single user only
- Operational constraints: should be maintainable by one person

## Open Questions

- Should abandoned books have a separate status in milestone 1?
- Is search needed immediately or can it wait?
