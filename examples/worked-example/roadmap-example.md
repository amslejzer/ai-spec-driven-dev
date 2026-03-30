# Roadmap Example

**Version:** 1.1  
**Date:** 2026-03-30  
**Status:** Worked example  
**Method Version:** 1.1

## Roadmap Summary

- Project state today: specification drafted, no code yet
- Next meaningful milestone: local-first MVP for tracking reading status
- Major dependencies: finalize first data model and basic flows

## Milestone 1

- Goal: create a usable local reading tracker
- Demo or completion signal: user can add books, update status, and review active and finished entries

### Phase 1

- Purpose: establish core data model and persistence
- Dependencies: specification sign-off

#### Task 1

- Goal: define storage shape and create basic entry persistence
- Checklist:
  - [ ] define entry fields
  - [ ] define status values
  - [ ] save entries locally

#### Task 2

- Goal: support add and edit flows
- Checklist:
  - [ ] create add flow
  - [ ] create edit flow
  - [ ] validate required fields

### Phase 2

- Purpose: add basic views for using the tracker daily
- Dependencies: entry persistence and editing

#### Task 3

- Goal: display books by status
- Checklist:
  - [ ] show to-read list
  - [ ] show reading list
  - [ ] show finished list

## Risks

- Risk 1: adding advanced metadata too early
- Risk 2: delaying task breakdown until implementation begins

## Notes

- Sequencing assumptions: data model comes before UI detail
- Deferred work: search, abandoned status, export
