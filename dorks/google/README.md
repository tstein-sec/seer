# Google Dork Lists

One file per application / platform. Every file:

1. Ranks dorks by ROI — **HIGH** (exposed data / credentials / unauth access) first,
   then **MEDIUM** (admin panels / debug surfaces / enumeration), then **LOW** (footprinting).
2. Cites a public source `[n]` for **every** line — no citation = no entry.
3. Ends with a **direct-path probe** section: verified sensitive paths to hit directly
   (these come from the same cited service checklists).

## Placeholders

- `{target}` / `{domain}` / `{company}` → your authorized scope (replace before searching).
- `{id}` / `{boardId}` → numeric IDs to iterate.

## Master source table

| # | Source | License/notes |
|---|--------|---------------|
| [1] | [Proviesec/google-dorks](https://github.com/Proviesec/google-dorks) | MIT; per-app dork files |
| [2] | [readloud/Google-Hacking-Database](https://github.com/readloud/Google-Hacking-Database) | GHDB archive + category dumps |
| [3] | [opsdisk/pagodo](https://github.com/opsdisk/pagodo) | GHDB-scraped dork files |
| [4] | [sushiwushi/bug-bounty-dorks](https://github.com/sushiwushi/bug-bounty-dorks) | Bug-bounty dork list |
| [5] | [BullsEye0/google_dork_list](https://github.com/BullsEye0/google_dork_list) | Large GHDB-style dump |
| [6] | [TakSec/google-dorks-bug-bounty](https://github.com/TakSec/google-dorks-bug-bounty) | Per-domain bug bounty dorks |
| [7] | [chr3st5an/Google-Dorking](https://github.com/chr3st5an/Google-Dorking) | Dorking cheat sheet |
| [8] | [Tobee1406/Awesome-Google-Dorks](https://github.com/Tobee1406/Awesome-Google-Dorks) | Curated dorks |
| [9] | [Exploit-DB GHDB](https://www.exploit-db.com/google-hacking-database) | Canonical GHDB |
| [10] | [DiddyMeech/Titan-Reborn](https://github.com/DiddyMeech/Titan-Reborn) | SaaS recon dork packs |
| [11] | [h0tak88r/Sec-88](https://github.com/h0tak88r/Sec-88) | Service-based pentest checklists; paths used as `inurl:` dorks |
| [12] | [xcode96/Google-Dorks](https://github.com/xcode96/Google-Dorks) | Platform dork catalog |
| [13] | [str1k3r0p/GoogleDorks](https://github.com/str1k3r0p/GoogleDorks) | Domain-scoped dork catalog |
| [14] | [D3v4nshPat3l/Dork-Ripper](https://github.com/D3v4nshPat3l/Dork-Ripper) | Dork lists by category |
| [15] | [root-Manas/webdorks](https://github.com/root-Manas/webdorks) | Per-goal dork packs |

## Adding a new app

1. Copy an existing file as template.
2. Keep the ROI tier order (HIGH → MEDIUM → LOW).
3. Every dork line: `dork [n]` where `[n]` is in the file header's Sources block.
4. Only include strings you can point to in a public source. Derivations from a
   verified string (e.g. wrapping in `site:{target}`) are allowed but must be obvious.
5. Run a grep for duplicates: `grep -rn "dork" dorks/google/ | sort | uniq -d`.
6. Update the coverage table in the root `README.md`.
