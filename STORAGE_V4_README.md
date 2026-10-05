# DayBook Storage v4

Storage is local-only and uses `localStorage`.

Keys:
- `daybook:v4:slotA`
- `daybook:v4:slotB`
- `daybook:v4:pointer`
- `daybook-v3` is read only for one-time migration.

Schema:
- `schemaVersion`
- `meta`: revision, createdAt, updatedAt
- `settings`: theme
- `days`: date keyed daily records
- `habits`: id, name, checks
- `goals`: id, name, progress
- `entries`: journal entries

Reliability:
1. Every write goes to the inactive slot first.
2. A checksum detects corrupted JSON snapshots.
3. On startup both slots are checked and the newest valid revision wins.
4. Existing v3 data is migrated automatically.
5. Export creates a clean v4 JSON backup.
6. Import validates the backup before replacing current data.

Important: localStorage is device/browser scoped. Clearing site data can delete it. Keep periodic exported backups if the journal matters.