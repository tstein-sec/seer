# seer 🔭

**Discovery-focused wordlists for web application reconnaissance.**

`seer` is a security wordlist project in the spirit of [SecLists](https://github.com/danielmiessler/SecLists), but purpose-built for **discovery**: finding the sensitive pages, exposed credentials, debug surfaces, and misconfigurations that actually matter when you are fingerprinting or attacking a web application.

Instead of generic "one big list" dumps, `seer` organizes wordlists **per application** (exactly like a top-100 web app inventory), and every list is:

- **Ranked by ROI** — the dorks with the highest hit-rate / highest severity sit at the top of each file.
- **Verified** — every entry comes from a real, publicly available collection (GHDB archives, well-known GitHub dork repositories, published pentest/handbook material) and carries a citation so nothing is hallucinated.
- **Discovery-focused** — strings are chosen to match sensitive *settings*, *config files*, *debug endpoints*, and *credential material* that only exist on sensitive pages.

## Repository layout

```
seer/
├── dorks/
│   ├── google/          # Google search dorks, one file per application
│   │   ├── wordpress.txt
│   │   ├── phpmyadmin.txt
│   │   ├── jenkins.txt
│   │   └── ...
│   ├── bing/            # (planned) Bing/DuckDuckGo equivalents
│   └── yandex/          # (planned)
├── fuzz/                # (planned) per-app fuzzing payloads / path lists
│   └── wordpress/
└── README.md
```

## How to read a dork file

Each file follows the same template:

```
### HIGH ROI — exposed data / credentials / unauthenticated access   <- run these first
dork-string [1]                                                       <- [n] = source
### MEDIUM ROI — admin panels / debug surfaces / user enumeration
...
### LOW ROI — footprinting / version detection
...
```

Citation keys are defined in the header of every file and map to public sources
(see `dorks/google/README.md` for the master source table).

**Placeholders** such as `{target}` or `{company}` mean *your authorized scope* —
replace them before searching.

## Verification policy

Contributions to `seer` **must**:

1. Include the dork exactly as it appears in a public, citable source (no memorized strings).
2. Cite the source per line (`[n]` pointing to the Sources section).
3. Place the dork in the correct ROI tier (highest ROI at the top).
4. Not include anything targeting a specific third party outside an authorized scope.

Sources used so far (top of the list = most used):

| # | Source | Notes |
|---|--------|-------|
| [1] | [Proviesec/google-dorks](https://github.com/Proviesec/google-dorks) | MIT; per-app dork files, actively updated |
| [2] | [readloud/Google-Hacking-Database](https://github.com/readloud/Google-Hacking-Database) | GHDB archive + category dumps |
| [3] | [opsdisk/pagodo](https://github.com/opsdisk/pagodo) | GHDB-scraped dork files |
| [4] | [sushiwushi/bug-bounty-dorks](https://github.com/sushiwushi/bug-bounty-dorks) | Bug-bounty dork list |
| [5] | [BullsEye0/google_dork_list](https://github.com/BullsEye0/google_dork_list) | Large GHDB-style dump |
| [6] | [TakSec/google-dorks-bug-bounty](https://github.com/TakSec/google-dorks-bug-bounty) | Per-domain bug bounty dorks |
| [7] | [chr3st5an/Google-Dorking](https://github.com/chr3st5an/Google-Dorking) | Google Dorking cheat sheet |
| [8] | [Tobee1406/Awesome-Google-Dorks](https://github.com/Tobee1406/Awesome-Google-Dorks) | Curated dork collection |
| [9] | [Exploit-DB Google Hacking Database](https://www.exploit-db.com/google-hacking-database) | Canonical GHDB |
| [10] | [DiddyMeech/Titan-Reborn](https://github.com/DiddyMeech/Titan-Reborn) | SaaS/recon dork packs |
| [11] | [h0tak88r/Sec-88](https://github.com/h0tak88r/Sec-88) | Service-based pentest checklists (paths used as `inurl:` dorks) |
| [12] | [xcode96/Google-Dorks](https://github.com/xcode96/Google-Dorks) | Platform dork catalog |
| [13] | [str1k3r0p/GoogleDorks](https://github.com/str1k3r0p/GoogleDorks) | Domain-scoped dork catalog |
| [14] | [D3v4nshPat3l/Dork-Ripper](https://github.com/D3v4nshPat3l/Dork-Ripper) | Dork lists by category |
| [15] | [root-Manas/webdorks](https://github.com/root-Manas/webdorks) | Per-goal dork packs (incl. DSN leaks) |

## Coverage (top-100 web apps — roadmap)

Current focus is the highest-value target set. Each app below maps to `dorks/google/<app>.txt`.
Apps marked `(planned)` are on the roadmap and need verified source material + citations before merging.

**CMS / web frameworks:** wordpress, joomla, drupal, magento, laravel, django, symfony (planned), rails (planned), typo3, contao, blogger (planned)

**Databases / admin panels:** phpmyadmin, mysql, mongodb, redis, postgresql, adminer, elasticsearch, couchdb (planned), cassandra (planned)

**DevOps / CI-CD / observability:** jenkins, gitlab, github-actions (planned), travis-ci (planned), circleci (planned), grafana, kibana, prometheus, sentry, sonarqube, nexus, rabbitmq, rancher, harbor (planned), vault (planned), consul (planned), airflow (planned), jupyterhub, metabase, splunk, zabbix, nagios (planned), cacti (planned)

**Cloud / SaaS:** aws, azure, gcp, firebase, slack, salesforce, hubspot, trello, bitbucket, confluence, jira, docker, kubernetes, openai (planned), stripe (planned), twilio (planned), sendgrid (planned), mailgun (planned)

**E-mail / office / hosting:** exchange-owa, roundcube (webmail), sharepoint, webmin, cpanel, plesk, tomcat, apache, nginx, phpinfo

## Contributing

1. Fork + PR against `main`.
2. One dork = one line = one citation. No citation, no merge.
3. Keep ROI ordering: secrets/data exposure > admin/debug surfaces > footprinting.
4. Add new app files under `dorks/google/` using the existing template.
5. Update the coverage table in this README when you add an app.

## Legal

These lists are for **authorized security testing and research only**. You are
responsible for complying with all applicable laws and with the target's policies.
The authors of `seer` are not liable for misuse. Dorking is passive, but acting on
what you find without authorization may be illegal.
