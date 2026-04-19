# Migration log — 2026-04-18

Executed at 2026-04-18 18:52.

Source-of-truth plan: `output/vault-audit-2026-04-18.md` (simplified strategy — keep Book Notes, archive everything else).

## Safety-rule overrides (user-authorised)

User explicitly overrode two CLAUDE.md safety rules:
- `Journal/*` → archived to `archive/Journal/` instead of protected `journal/` path
- `Assets/*` → archived to `archive/Assets/` instead of protected `assets/` path

Rationale: park-and-triage migration. Content is preserved in `archive/`, not deleted.

## Summary

- Migrated: 63
- Archived: 313
- Trashed: 0
- Deferred to `inbox/review/`: 0

## Migrated (63) — Book Notes

Folder-level move: `3. Resources/Book Notes/` → `sources/learning/books/` (renamed during `mv`; full subtree preserved, including `Kindle Highlights/` 58 files and `My Notes/` 3 files).

- `3. Resources/Book Notes/Ikigai.md` → `sources/learning/books/Ikigai.md`
- `3. Resources/Book Notes/Kindle Highlights/Albom-Tuesdays With Morrie.md` → `sources/learning/books/Kindle Highlights/Albom-Tuesdays With Morrie.md`
- `3. Resources/Book Notes/Kindle Highlights/Ariely-Predictably Irrational.md` → `sources/learning/books/Kindle Highlights/Ariely-Predictably Irrational.md`
- `3. Resources/Book Notes/Kindle Highlights/Asher-Thirteen Reasons Why.md` → `sources/learning/books/Kindle Highlights/Asher-Thirteen Reasons Why.md`
- `3. Resources/Book Notes/Kindle Highlights/Austen-Pride and Prejudice.md` → `sources/learning/books/Kindle Highlights/Austen-Pride and Prejudice.md`
- `3. Resources/Book Notes/Kindle Highlights/Backman-And Every Morning the Way Home Gets Longer and Longer.md` → `sources/learning/books/Kindle Highlights/Backman-And Every Morning the Way Home Gets Longer and Longer.md`
- `3. Resources/Book Notes/Kindle Highlights/Blank-The Four Steps to the Epiphany.md` → `sources/learning/books/Kindle Highlights/Blank-The Four Steps to the Epiphany.md`
- `3. Resources/Book Notes/Kindle Highlights/Brown-Origin.md` → `sources/learning/books/Kindle Highlights/Brown-Origin.md`
- `3. Resources/Book Notes/Kindle Highlights/Brown-The Da Vinci Code.md` → `sources/learning/books/Kindle Highlights/Brown-The Da Vinci Code.md`
- `3. Resources/Book Notes/Kindle Highlights/Byrne-The Secret.md` → `sources/learning/books/Kindle Highlights/Byrne-The Secret.md`
- `3. Resources/Book Notes/Kindle Highlights/Cannon-Linux for Beginners.md` → `sources/learning/books/Kindle Highlights/Cannon-Linux for Beginners.md`
- `3. Resources/Book Notes/Kindle Highlights/Carnegie-How to Win Friends and Influence People.md` → `sources/learning/books/Kindle Highlights/Carnegie-How to Win Friends and Influence People.md`
- `3. Resources/Book Notes/Kindle Highlights/Christie-And Then There Were None.md` → `sources/learning/books/Kindle Highlights/Christie-And Then There Were None.md`
- `3. Resources/Book Notes/Kindle Highlights/Coelho-Sanches-The Pilgrimage.md` → `sources/learning/books/Kindle Highlights/Coelho-Sanches-The Pilgrimage.md`
- `3. Resources/Book Notes/Kindle Highlights/Coelho-The Alchemist.md` → `sources/learning/books/Kindle Highlights/Coelho-The Alchemist.md`
- `3. Resources/Book Notes/Kindle Highlights/Collins-Catching Fire.md` → `sources/learning/books/Kindle Highlights/Collins-Catching Fire.md`
- `3. Resources/Book Notes/Kindle Highlights/Collins-Mockingjay.md` → `sources/learning/books/Kindle Highlights/Collins-Mockingjay.md`
- `3. Resources/Book Notes/Kindle Highlights/Collins-The Hunger Games.md` → `sources/learning/books/Kindle Highlights/Collins-The Hunger Games.md`
- `3. Resources/Book Notes/Kindle Highlights/DeMarco-The Millionaire Fastlane.md` → `sources/learning/books/Kindle Highlights/DeMarco-The Millionaire Fastlane.md`
- `3. Resources/Book Notes/Kindle Highlights/Doerr-All the Light We Cannot See.md` → `sources/learning/books/Kindle Highlights/Doerr-All the Light We Cannot See.md`
- `3. Resources/Book Notes/Kindle Highlights/Fitzgerald-The Great Gatsby.md` → `sources/learning/books/Kindle Highlights/Fitzgerald-The Great Gatsby.md`
- `3. Resources/Book Notes/Kindle Highlights/Frankl-Mans Search For Meaning.md` → `sources/learning/books/Kindle Highlights/Frankl-Mans Search For Meaning.md`
- `3. Resources/Book Notes/Kindle Highlights/Gaarder-Sophies World.md` → `sources/learning/books/Kindle Highlights/Gaarder-Sophies World.md`
- `3. Resources/Book Notes/Kindle Highlights/Gilbert-Eat Pray Love.md` → `sources/learning/books/Kindle Highlights/Gilbert-Eat Pray Love.md`
- `3. Resources/Book Notes/Kindle Highlights/Gray-Men Are from Mars, Women Are from Venus.md` → `sources/learning/books/Kindle Highlights/Gray-Men Are from Mars, Women Are from Venus.md`
- `3. Resources/Book Notes/Kindle Highlights/Green-Looking For Alaska.md` → `sources/learning/books/Kindle Highlights/Green-Looking For Alaska.md`
- `3. Resources/Book Notes/Kindle Highlights/Green-Turtles All the Way Down-1720089041995.md` → `sources/learning/books/Kindle Highlights/Green-Turtles All the Way Down-1720089041995.md`
- `3. Resources/Book Notes/Kindle Highlights/Green-Turtles All the Way Down.md` → `sources/learning/books/Kindle Highlights/Green-Turtles All the Way Down.md`
- `3. Resources/Book Notes/Kindle Highlights/Greene-The 48 Laws Of Power.md` → `sources/learning/books/Kindle Highlights/Greene-The 48 Laws Of Power.md`
- `3. Resources/Book Notes/Kindle Highlights/Gregg-Systems Performance-1720089025892.md` → `sources/learning/books/Kindle Highlights/Gregg-Systems Performance-1720089025892.md`
- `3. Resources/Book Notes/Kindle Highlights/Gregg-Systems Performance.md` → `sources/learning/books/Kindle Highlights/Gregg-Systems Performance.md`
- `3. Resources/Book Notes/Kindle Highlights/Guillebeau-The $100 Startup.md` → `sources/learning/books/Kindle Highlights/Guillebeau-The $100 Startup.md`
- `3. Resources/Book Notes/Kindle Highlights/Hawking-A Brief History Of Time.md` → `sources/learning/books/Kindle Highlights/Hawking-A Brief History Of Time.md`
- `3. Resources/Book Notes/Kindle Highlights/Hesse-Siddhartha.md` → `sources/learning/books/Kindle Highlights/Hesse-Siddhartha.md`
- `3. Resources/Book Notes/Kindle Highlights/Kleppmann-Designing Data-Intensive Applications.md` → `sources/learning/books/Kindle Highlights/Kleppmann-Designing Data-Intensive Applications.md`
- `3. Resources/Book Notes/Kindle Highlights/Lee-To Kill A Mockingbird.md` → `sources/learning/books/Kindle Highlights/Lee-To Kill A Mockingbird.md`
- `3. Resources/Book Notes/Kindle Highlights/Lowndes-How to Talk to Anyone.md` → `sources/learning/books/Kindle Highlights/Lowndes-How to Talk to Anyone.md`
- `3. Resources/Book Notes/Kindle Highlights/McGilchrist-The Master and His Emissary.md` → `sources/learning/books/Kindle Highlights/McGilchrist-The Master and His Emissary.md`
- `3. Resources/Book Notes/Kindle Highlights/Mulcahy-The Gig Economy.md` → `sources/learning/books/Kindle Highlights/Mulcahy-The Gig Economy.md`
- `3. Resources/Book Notes/Kindle Highlights/Murphy_et_al-Site Reliability Engineering.md` → `sources/learning/books/Kindle Highlights/Murphy_et_al-Site Reliability Engineering.md`
- `3. Resources/Book Notes/Kindle Highlights/Myers-Myers-Gifts Differing.md` → `sources/learning/books/Kindle Highlights/Myers-Myers-Gifts Differing.md`
- `3. Resources/Book Notes/Kindle Highlights/Niven-All the Bright Places.md` → `sources/learning/books/Kindle Highlights/Niven-All the Bright Places.md`
- `3. Resources/Book Notes/Kindle Highlights/Orwell-Animal Farm.md` → `sources/learning/books/Kindle Highlights/Orwell-Animal Farm.md`
- `3. Resources/Book Notes/Kindle Highlights/Rowell-Eleanor & Park.md` → `sources/learning/books/Kindle Highlights/Rowell-Eleanor & Park.md`
- `3. Resources/Book Notes/Kindle Highlights/Sharma-The Monk Who Sold His Ferrari.md` → `sources/learning/books/Kindle Highlights/Sharma-The Monk Who Sold His Ferrari.md`
- `3. Resources/Book Notes/Kindle Highlights/Sinek-Leaders Eat Last-1720089017894.md` → `sources/learning/books/Kindle Highlights/Sinek-Leaders Eat Last-1720089017894.md`
- `3. Resources/Book Notes/Kindle Highlights/Sinek-Leaders Eat Last.md` → `sources/learning/books/Kindle Highlights/Sinek-Leaders Eat Last.md`
- `3. Resources/Book Notes/Kindle Highlights/Sinek-Start With Why-1720089033897.md` → `sources/learning/books/Kindle Highlights/Sinek-Start With Why-1720089033897.md`
- `3. Resources/Book Notes/Kindle Highlights/Sinek-Start With Why.md` → `sources/learning/books/Kindle Highlights/Sinek-Start With Why.md`
- `3. Resources/Book Notes/Kindle Highlights/Thomas-The Big Switch.md` → `sources/learning/books/Kindle Highlights/Thomas-The Big Switch.md`
- `3. Resources/Book Notes/Kindle Highlights/Todd-After.md` → `sources/learning/books/Kindle Highlights/Todd-After.md`
- `3. Resources/Book Notes/Kindle Highlights/Tuhovsky-Editing-Communication Skills Training.md` → `sources/learning/books/Kindle Highlights/Tuhovsky-Editing-Communication Skills Training.md`
- `3. Resources/Book Notes/Kindle Highlights/Walton-A Practical Guide to Emotional Intelligence.md` → `sources/learning/books/Kindle Highlights/Walton-A Practical Guide to Emotional Intelligence.md`
- `3. Resources/Book Notes/Kindle Highlights/Watt-A Practical Guide to Mindfulness.md` → `sources/learning/books/Kindle Highlights/Watt-A Practical Guide to Mindfulness.md`
- `3. Resources/Book Notes/Kindle Highlights/Xu-System Design Interview – An insiders guide.md` → `sources/learning/books/Kindle Highlights/Xu-System Design Interview – An insiders guide.md`
- `3. Resources/Book Notes/Kindle Highlights/Yogananda-God Talks with Arjuna The Bhagavad Gita.md` → `sources/learning/books/Kindle Highlights/Yogananda-God Talks with Arjuna The Bhagavad Gita.md`
- `3. Resources/Book Notes/Kindle Highlights/Yoon-The Sun is also a Star.md` → `sources/learning/books/Kindle Highlights/Yoon-The Sun is also a Star.md`
- `3. Resources/Book Notes/Kindle Highlights/Zafon-The Shadow Of The Wind.md` → `sources/learning/books/Kindle Highlights/Zafon-The Shadow Of The Wind.md`
- `3. Resources/Book Notes/Kindle Highlights/Zusak-The Book Thief.md` → `sources/learning/books/Kindle Highlights/Zusak-The Book Thief.md`
- `3. Resources/Book Notes/My Notes/Sophie's World.md` → `sources/learning/books/My Notes/Sophie's World.md`
- `3. Resources/Book Notes/My Notes/The million dollar weekend.md` → `sources/learning/books/My Notes/The million dollar weekend.md`
- `3. Resources/Book Notes/My Notes/The Millionaire Fastlane.md` → `sources/learning/books/My Notes/The Millionaire Fastlane.md`
- `3. Resources/Book Notes/System Performance by Brendon Gregg.md` → `sources/learning/books/System Performance by Brendon Gregg.md`

## Archived (313)

Folder-level moves (bulk `mv`, subtrees preserved):

| Source | Target | .md files |
|---|---|---|
| `1. Projects/` | `archive/1. Projects/` | 22 |
| `2. Areas/` | `archive/2. Areas/` | 71 |
| `3. Resources/` (Book Notes removed first) | `archive/3. Resources/` | 74 |
| `4. Archives/` | `archive/4. Archives/` | 7 |
| `Journal/` | `archive/Journal/` | 88 (override) |
| `Meeting Notes/` | `archive/Meeting Notes/` | 6 |
| `Assets/` | `archive/Assets/` | 1 md + images (override) |
| `Ink/` | `archive/Ink/` | 0 (empty dir preserved) |
| `Scratch Pad/` | `archive/Scratch Pad/` | 0 (empty dir preserved) |
| 44 root-level loose `.md` files | `archive/loose/` | 44 |

### Full archived-file manifest

- `1. Projects/Alerts Cleanup.md` → `archive/1. Projects/Alerts Cleanup.md`
- `1. Projects/Api Gateway's Use for Third Party API's Integrations.md` → `archive/1. Projects/Api Gateway's Use for Third Party API's Integrations.md`
- `1. Projects/APM Optimizations/Optimize Elastic Search.md` → `archive/1. Projects/APM Optimizations/Optimize Elastic Search.md`
- `1. Projects/Automated RCA's.md` → `archive/1. Projects/Automated RCA's.md`
- `1. Projects/Bamboo Upgrade.md` → `archive/1. Projects/Bamboo Upgrade.md`
- `1. Projects/BitBucket Cloud Migration.md` → `archive/1. Projects/BitBucket Cloud Migration.md`
- `1. Projects/CCMS Secrets/CCMS secrets.md` → `archive/1. Projects/CCMS Secrets/CCMS secrets.md`
- `1. Projects/Chaos Engineering/Automated Chaos engineering.md` → `archive/1. Projects/Chaos Engineering/Automated Chaos engineering.md`
- `1. Projects/Clean up Alerting.md` → `archive/1. Projects/Clean up Alerting.md`
- `1. Projects/Debugging Scripts.md` → `archive/1. Projects/Debugging Scripts.md`
- `1. Projects/Debugging Scripts/Debugging Script.md` → `archive/1. Projects/Debugging Scripts/Debugging Script.md`
- `1. Projects/Debugging Scripts/Debugging Scripts.md` → `archive/1. Projects/Debugging Scripts/Debugging Scripts.md`
- `1. Projects/Disaster Recovery.md` → `archive/1. Projects/Disaster Recovery.md`
- `1. Projects/Global Circuit Breaker/Global circuit breaker.md` → `archive/1. Projects/Global Circuit Breaker/Global circuit breaker.md`
- `1. Projects/Istio Observability/Istio Observability.md` → `archive/1. Projects/Istio Observability/Istio Observability.md`
- `1. Projects/Istio Observability/Istio Proxy Access Logs.md` → `archive/1. Projects/Istio Observability/Istio Proxy Access Logs.md`
- `1. Projects/Project Dashboard.md` → `archive/1. Projects/Project Dashboard.md`
- `1. Projects/SRE Vision/Apr-May-June.md` → `archive/1. Projects/SRE Vision/Apr-May-June.md`
- `1. Projects/SRE Vision/SRE Vision.md` → `archive/1. Projects/SRE Vision/SRE Vision.md`
- `1. Projects/SRI Lanka SIT Env Migration.md` → `archive/1. Projects/SRI Lanka SIT Env Migration.md`
- `1. Projects/Untitled 1.md` → `archive/1. Projects/Untitled 1.md`
- `1. Projects/Untitled.md` → `archive/1. Projects/Untitled.md`
- `2. Areas/Arch Review/Amazon dump api.md` → `archive/2. Areas/Arch Review/Amazon dump api.md`
- `2. Areas/Arch Review/Android Arch Review.md` → `archive/2. Areas/Arch Review/Android Arch Review.md`
- `2. Areas/Arch Review/BMS Arch Meets/9th Oct 2023.md` → `archive/2. Areas/Arch Review/BMS Arch Meets/9th Oct 2023.md`
- `2. Areas/Arch Review/BMS Arch Meets/AI Applications in BMS.md` → `archive/2. Areas/Arch Review/BMS Arch Meets/AI Applications in BMS.md`
- `2. Areas/Arch Review/BMS Arch Meets/BMS Arch Meets.md` → `archive/2. Areas/Arch Review/BMS Arch Meets/BMS Arch Meets.md`
- `2. Areas/Arch Review/BMS Arch Meets/Fault Tolerance across BMS.md` → `archive/2. Areas/Arch Review/BMS Arch Meets/Fault Tolerance across BMS.md`
- `2. Areas/Arch Review/BMS Arch Meets/Principal Engineers Weekly Catch-up (8th Jan).md` → `archive/2. Areas/Arch Review/BMS Arch Meets/Principal Engineers Weekly Catch-up (8th Jan).md`
- `2. Areas/Arch Review/BMS Arch Meets/SRE 1.md` → `archive/2. Areas/Arch Review/BMS Arch Meets/SRE 1.md`
- `2. Areas/Arch Review/DataOpsSeatOcc High Level Arch Review.md` → `archive/2. Areas/Arch Review/DataOpsSeatOcc High Level Arch Review.md`
- `2. Areas/Arch Review/Discovery Arch Review.md` → `archive/2. Areas/Arch Review/Discovery Arch Review.md`
- `2. Areas/Arch Review/LE.md` → `archive/2. Areas/Arch Review/LE.md`
- `2. Areas/Arch Review/Scalability.md` → `archive/2. Areas/Arch Review/Scalability.md`
- `2. Areas/Arch Review/Security.md` → `archive/2. Areas/Arch Review/Security.md`
- `2. Areas/Architecture Review/Retention of req-resp of external payment APIs.md` → `archive/2. Areas/Architecture Review/Retention of req-resp of external payment APIs.md`
- `2. Areas/Communication/First Impressions.md` → `archive/2. Areas/Communication/First Impressions.md`
- `2. Areas/Communication/Someone likes you.md` → `archive/2. Areas/Communication/Someone likes you.md`
- `2. Areas/Communication/Think Fast Talk Smart.md` → `archive/2. Areas/Communication/Think Fast Talk Smart.md`
- `2. Areas/Finances/Investments/Industries/Auto.md` → `archive/2. Areas/Finances/Investments/Industries/Auto.md`
- `2. Areas/Finances/Investments/Industries/Battery.md` → `archive/2. Areas/Finances/Investments/Industries/Battery.md`
- `2. Areas/Finances/Investments/Industries/Consumer Products.md` → `archive/2. Areas/Finances/Investments/Industries/Consumer Products.md`
- `2. Areas/Finances/Investments/Industries/copper.md` → `archive/2. Areas/Finances/Investments/Industries/copper.md`
- `2. Areas/Finances/Investments/Industries/E-Commerce.md` → `archive/2. Areas/Finances/Investments/Industries/E-Commerce.md`
- `2. Areas/Finances/Investments/Industries/Electronics.md` → `archive/2. Areas/Finances/Investments/Industries/Electronics.md`
- `2. Areas/Finances/Investments/Industries/EV.md` → `archive/2. Areas/Finances/Investments/Industries/EV.md`
- `2. Areas/Finances/Investments/Industries/Gen-Z.md` → `archive/2. Areas/Finances/Investments/Industries/Gen-Z.md`
- `2. Areas/Finances/Investments/Industries/Health care.md` → `archive/2. Areas/Finances/Investments/Industries/Health care.md`
- `2. Areas/Finances/Investments/Industries/Hospitals.md` → `archive/2. Areas/Finances/Investments/Industries/Hospitals.md`
- `2. Areas/Finances/Investments/Industries/Ice cream.md` → `archive/2. Areas/Finances/Investments/Industries/Ice cream.md`
- `2. Areas/Finances/Investments/Industries/Infrastructure.md` → `archive/2. Areas/Finances/Investments/Industries/Infrastructure.md`
- `2. Areas/Finances/Investments/Industries/IT.md` → `archive/2. Areas/Finances/Investments/Industries/IT.md`
- `2. Areas/Finances/Investments/Industries/Public Sector  Units.md` → `archive/2. Areas/Finances/Investments/Industries/Public Sector  Units.md`
- `2. Areas/Finances/Investments/Industries/Quick Commerce.md` → `archive/2. Areas/Finances/Investments/Industries/Quick Commerce.md`
- `2. Areas/Finances/Investments/Industries/Renewables.md` → `archive/2. Areas/Finances/Investments/Industries/Renewables.md`
- `2. Areas/Finances/Investments/Industries/services.md` → `archive/2. Areas/Finances/Investments/Industries/services.md`
- `2. Areas/Finances/Investments/Industries/Solar.md` → `archive/2. Areas/Finances/Investments/Industries/Solar.md`
- `2. Areas/Finances/Investments/Industries/Steel.md` → `archive/2. Areas/Finances/Investments/Industries/Steel.md`
- `2. Areas/Finances/Investments/Industries/Sugar.md` → `archive/2. Areas/Finances/Investments/Industries/Sugar.md`
- `2. Areas/Finances/Investments/Learn/Anual Report.md` → `archive/2. Areas/Finances/Investments/Learn/Anual Report.md`
- `2. Areas/Finances/Investments/Learn/Balance Sheets.md` → `archive/2. Areas/Finances/Investments/Learn/Balance Sheets.md`
- `2. Areas/Finances/Investments/Learn/Financial Ratios.md` → `archive/2. Areas/Finances/Investments/Learn/Financial Ratios.md`
- `2. Areas/Finances/Investments/Learn/Fundamental Analysis.md` → `archive/2. Areas/Finances/Investments/Learn/Fundamental Analysis.md`
- `2. Areas/Finances/Investments/Learn/How to make 1cr.md` → `archive/2. Areas/Finances/Investments/Learn/How to make 1cr.md`
- `2. Areas/Finances/Investments/Learn/How to pick small caps.md` → `archive/2. Areas/Finances/Investments/Learn/How to pick small caps.md`
- `2. Areas/Finances/Investments/Learn/Income Statrement.md` → `archive/2. Areas/Finances/Investments/Learn/Income Statrement.md`
- `2. Areas/Finances/Investments/Learn/Moat.md` → `archive/2. Areas/Finances/Investments/Learn/Moat.md`
- `2. Areas/Finances/Investments/Learn/Solc/Basic Finance (conflict 2024-12-18-10-38-38).md` → `archive/2. Areas/Finances/Investments/Learn/Solc/Basic Finance (conflict 2024-12-18-10-38-38).md`
- `2. Areas/Finances/Investments/Learn/Solc/Basic Finance.md` → `archive/2. Areas/Finances/Investments/Learn/Solc/Basic Finance.md`
- `2. Areas/Finances/Investments/Stocks/Dee dev.md` → `archive/2. Areas/Finances/Investments/Stocks/Dee dev.md`
- `2. Areas/Finances/Investments/Stocks/Delta Corp.md` → `archive/2. Areas/Finances/Investments/Stocks/Delta Corp.md`
- `2. Areas/Finances/Investments/Stocks/Dipak Nitrate.md` → `archive/2. Areas/Finances/Investments/Stocks/Dipak Nitrate.md`
- `2. Areas/Finances/Investments/Stocks/Fine Organics.md` → `archive/2. Areas/Finances/Investments/Stocks/Fine Organics.md`
- `2. Areas/Finances/Investments/Stocks/GPIL.md` → `archive/2. Areas/Finances/Investments/Stocks/GPIL.md`
- `2. Areas/Finances/Investments/Stocks/Himadri Specialty Chemicals.md` → `archive/2. Areas/Finances/Investments/Stocks/Himadri Specialty Chemicals.md`
- `2. Areas/Finances/Investments/Stocks/Integra.md` → `archive/2. Areas/Finances/Investments/Stocks/Integra.md`
- `2. Areas/Finances/Investments/Stocks/IRFC.md` → `archive/2. Areas/Finances/Investments/Stocks/IRFC.md`
- `2. Areas/Finances/Investments/Stocks/List.md` → `archive/2. Areas/Finances/Investments/Stocks/List.md`
- `2. Areas/Finances/Investments/Stocks/Nuvava wealth management.md` → `archive/2. Areas/Finances/Investments/Stocks/Nuvava wealth management.md`
- `2. Areas/Finances/Investments/Stocks/Party Cruisers.md` → `archive/2. Areas/Finances/Investments/Stocks/Party Cruisers.md`
- `2. Areas/Finances/Investments/Stocks/Praveg.md` → `archive/2. Areas/Finances/Investments/Stocks/Praveg.md`
- `2. Areas/Finances/Investments/Stocks/Reliance.md` → `archive/2. Areas/Finances/Investments/Stocks/Reliance.md`
- `2. Areas/Finances/Investments/Stocks/Rushil Decor.md` → `archive/2. Areas/Finances/Investments/Stocks/Rushil Decor.md`
- `2. Areas/Finances/Investments/Stocks/SMCI.md` → `archive/2. Areas/Finances/Investments/Stocks/SMCI.md`
- `2. Areas/Passive Income/Ideas.md` → `archive/2. Areas/Passive Income/Ideas.md`
- `2. Areas/Passive Income/Passive income.md` → `archive/2. Areas/Passive Income/Passive income.md`
- `2. Areas/Photography/Depth of field.md` → `archive/2. Areas/Photography/Depth of field.md`
- `2. Areas/Reading List/Articles.md` → `archive/2. Areas/Reading List/Articles.md`
- `2. Areas/SRE Highlights/2023-03.md` → `archive/2. Areas/SRE Highlights/2023-03.md`
- `2. Areas/SRE Highlights/2023-04.md` → `archive/2. Areas/SRE Highlights/2023-04.md`
- `2. Areas/Thirdparty Tools/Datadog.md` → `archive/2. Areas/Thirdparty Tools/Datadog.md`
- `2. Areas/Thirdparty Tools/OpsTree Build piper demo.md` → `archive/2. Areas/Thirdparty Tools/OpsTree Build piper demo.md`
- `2. Areas/Thirdparty Tools/Signadot.md` → `archive/2. Areas/Thirdparty Tools/Signadot.md`
- `3. Resources/Articles/Body Language.md` → `archive/3. Resources/Articles/Body Language.md`
- `3. Resources/Computer Science/Architecture/Logging VS Distributed Tracing.md` → `archive/3. Resources/Computer Science/Architecture/Logging VS Distributed Tracing.md`
- `3. Resources/Computer Science/Artificial Intelligence/Back propogation.md` → `archive/3. Resources/Computer Science/Artificial Intelligence/Back propogation.md`
- `3. Resources/Computer Science/Artificial Intelligence/Reading Material.md` → `archive/3. Resources/Computer Science/Artificial Intelligence/Reading Material.md`
- `3. Resources/Computer Science/Artificial Intelligence/Stanford course on AI & ML.md` → `archive/3. Resources/Computer Science/Artificial Intelligence/Stanford course on AI & ML.md`
- `3. Resources/Computer Science/AWS/EBS Application consistent backups.md` → `archive/3. Resources/Computer Science/AWS/EBS Application consistent backups.md`
- `3. Resources/Computer Science/Best Practices/Code Review.md` → `archive/3. Resources/Computer Science/Best Practices/Code Review.md`
- `3. Resources/Computer Science/Best Practices/K8s Container Security.md` → `archive/3. Resources/Computer Science/Best Practices/K8s Container Security.md`
- `3. Resources/Computer Science/Debugging/AWS cli cheat sheet.md` → `archive/3. Resources/Computer Science/Debugging/AWS cli cheat sheet.md`
- `3. Resources/Computer Science/Debugging/AWS Debugging.md` → `archive/3. Resources/Computer Science/Debugging/AWS Debugging.md`
- `3. Resources/Computer Science/Debugging/Cinema websites issue.md` → `archive/3. Resources/Computer Science/Debugging/Cinema websites issue.md`
- `3. Resources/Computer Science/Debugging/Git cheat-sheet.md` → `archive/3. Resources/Computer Science/Debugging/Git cheat-sheet.md`
- `3. Resources/Computer Science/Debugging/Istio Debugging.md` → `archive/3. Resources/Computer Science/Debugging/Istio Debugging.md`
- `3. Resources/Computer Science/Debugging/Istio Issues/Istio GRPC issue cx-chatbot-api to mt-ticketing-cancellation.md` → `archive/3. Resources/Computer Science/Debugging/Istio Issues/Istio GRPC issue cx-chatbot-api to mt-ticketing-cancellation.md`
- `3. Resources/Computer Science/Debugging/Istio Issues/Istio GRPC pg-order-sumary --> members-main-app.md` → `archive/3. Resources/Computer Science/Debugging/Istio Issues/Istio GRPC pg-order-sumary --> members-main-app.md`
- `3. Resources/Computer Science/Debugging/Istio Issues/Virtual service Canary debugging.md` → `archive/3. Resources/Computer Science/Debugging/Istio Issues/Virtual service Canary debugging.md`
- `3. Resources/Computer Science/Debugging/Kubectl cheat-sheet.md` → `archive/3. Resources/Computer Science/Debugging/Kubectl cheat-sheet.md`
- `3. Resources/Computer Science/Debugging/Kubernetes/node spike issue.md` → `archive/3. Resources/Computer Science/Debugging/Kubernetes/node spike issue.md`
- `3. Resources/Computer Science/Debugging/Kubernetes/Setup CloudWatch Agent in EKS.md` → `archive/3. Resources/Computer Science/Debugging/Kubernetes/Setup CloudWatch Agent in EKS.md`
- `3. Resources/Computer Science/Debugging/Linux cheat-sheet.md` → `archive/3. Resources/Computer Science/Debugging/Linux cheat-sheet.md`
- `3. Resources/Computer Science/Debugging/Linux Network Debug.md` → `archive/3. Resources/Computer Science/Debugging/Linux Network Debug.md`
- `3. Resources/Computer Science/Debugging/Prometheus Cheat Sheet.md` → `archive/3. Resources/Computer Science/Debugging/Prometheus Cheat Sheet.md`
- `3. Resources/Computer Science/Debugging/RabbitMq Commands.md` → `archive/3. Resources/Computer Science/Debugging/RabbitMq Commands.md`
- `3. Resources/Computer Science/Disaster Recovery/Appranix vs Nimesa.md` → `archive/3. Resources/Computer Science/Disaster Recovery/Appranix vs Nimesa.md`
- `3. Resources/Computer Science/Disaster Recovery/DataMotive POC.md` → `archive/3. Resources/Computer Science/Disaster Recovery/DataMotive POC.md`
- `3. Resources/Computer Science/Disaster Recovery/Disaster Recovery.md` → `archive/3. Resources/Computer Science/Disaster Recovery/Disaster Recovery.md`
- `3. Resources/Computer Science/Disaster Recovery/Nemisa.md` → `archive/3. Resources/Computer Science/Disaster Recovery/Nemisa.md`
- `3. Resources/Computer Science/Disaster Recovery/Session Notes.md` → `archive/3. Resources/Computer Science/Disaster Recovery/Session Notes.md`
- `3. Resources/Computer Science/Ideas.md` → `archive/3. Resources/Computer Science/Ideas.md`
- `3. Resources/Computer Science/Linux/eBPF/To Check.md` → `archive/3. Resources/Computer Science/Linux/eBPF/To Check.md`
- `3. Resources/Computer Science/Linux/Mount more then 2TB disk.md` → `archive/3. Resources/Computer Science/Linux/Mount more then 2TB disk.md`
- `3. Resources/Computer Science/Performance Issues/CPU.md` → `archive/3. Resources/Computer Science/Performance Issues/CPU.md`
- `3. Resources/Computer Science/Performance Issues/Methodologies.md` → `archive/3. Resources/Computer Science/Performance Issues/Methodologies.md`
- `3. Resources/Computer Science/Reading List.md` → `archive/3. Resources/Computer Science/Reading List.md`
- `3. Resources/Computer Science/System Design/Design Patterns/store and forward.md` → `archive/3. Resources/Computer Science/System Design/Design Patterns/store and forward.md`
- `3. Resources/Computer Science/Technologies/Aerospike.md` → `archive/3. Resources/Computer Science/Technologies/Aerospike.md`
- `3. Resources/Computer Science/Technologies/ElasticSearch.md` → `archive/3. Resources/Computer Science/Technologies/ElasticSearch.md`
- `3. Resources/Computer Science/Technologies/Mongo DB.md` → `archive/3. Resources/Computer Science/Technologies/Mongo DB.md`
- `3. Resources/Computer Science/Technologies/MySql.md` → `archive/3. Resources/Computer Science/Technologies/MySql.md`
- `3. Resources/Computer Science/Technologies/Redis.md` → `archive/3. Resources/Computer Science/Technologies/Redis.md`
- `3. Resources/Computer Science/Workshops/Storage Engine.md` → `archive/3. Resources/Computer Science/Workshops/Storage Engine.md`
- `3. Resources/Debugging Tricks/Intall debug tools ebpf.md` → `archive/3. Resources/Debugging Tricks/Intall debug tools ebpf.md`
- `3. Resources/Intersting Concepts-Ideas/Framing Bias.md` → `archive/3. Resources/Intersting Concepts-Ideas/Framing Bias.md`
- `3. Resources/Intersting Concepts-Ideas/Murphys Law.md` → `archive/3. Resources/Intersting Concepts-Ideas/Murphys Law.md`
- `3. Resources/Intersting Concepts-Ideas/Pygmalion Effect.md` → `archive/3. Resources/Intersting Concepts-Ideas/Pygmalion Effect.md`
- `3. Resources/Issues & RCA/Dunki & Salar Traffic.md` → `archive/3. Resources/Issues & RCA/Dunki & Salar Traffic.md`
- `3. Resources/Management/Innovation is not efficient.md` → `archive/3. Resources/Management/Innovation is not efficient.md`
- `3. Resources/Management/Law of Diffusion.md` → `archive/3. Resources/Management/Law of Diffusion.md`
- `3. Resources/Management/Team Building.md` → `archive/3. Resources/Management/Team Building.md`
- `3. Resources/Management/Tips.md` → `archive/3. Resources/Management/Tips.md`
- `3. Resources/Meeting Notes/DB-Governance/Database Governance 8th Jan.md` → `archive/3. Resources/Meeting Notes/DB-Governance/Database Governance 8th Jan.md`
- `3. Resources/Meeting Notes/DR/Action Plan for DR.md` → `archive/3. Resources/Meeting Notes/DR/Action Plan for DR.md`
- `3. Resources/Meeting Notes/DR/Appranix Bookmyshow Application Consistency call.md` → `archive/3. Resources/Meeting Notes/DR/Appranix Bookmyshow Application Consistency call.md`
- `3. Resources/Meeting Notes/DR/Appranix Bookmyshow Doubts call.md` → `archive/3. Resources/Meeting Notes/DR/Appranix Bookmyshow Doubts call.md`
- `3. Resources/Meeting Notes/Max connections on DB's.md` → `archive/3. Resources/Meeting Notes/Max connections on DB's.md`
- `3. Resources/Meeting Notes/Prometheus related doubts for SR metrics.md` → `archive/3. Resources/Meeting Notes/Prometheus related doubts for SR metrics.md`
- `3. Resources/People/Arvin Mathias.md` → `archive/3. Resources/People/Arvin Mathias.md`
- `3. Resources/People/Avani Singhal.md` → `archive/3. Resources/People/Avani Singhal.md`
- `3. Resources/People/Kadambini Tendulkar.md` → `archive/3. Resources/People/Kadambini Tendulkar.md`
- `3. Resources/People/Kamal Rohra.md` → `archive/3. Resources/People/Kamal Rohra.md`
- `3. Resources/People/Marlin Shah.md` → `archive/3. Resources/People/Marlin Shah.md`
- `3. Resources/People/Mohini.md` → `archive/3. Resources/People/Mohini.md`
- `3. Resources/People/Moiz.md` → `archive/3. Resources/People/Moiz.md`
- `3. Resources/People/Ralstan Vaz.md` → `archive/3. Resources/People/Ralstan Vaz.md`
- `3. Resources/People/Riyaz Manihar.md` → `archive/3. Resources/People/Riyaz Manihar.md`
- `3. Resources/People/Viraj Bharvada.md` → `archive/3. Resources/People/Viraj Bharvada.md`
- `3. Resources/People/Viraj.md` → `archive/3. Resources/People/Viraj.md`
- `3. Resources/People/Wali.md` → `archive/3. Resources/People/Wali.md`
- `3. Resources/Philosophy/Relationship/Relationship.md` → `archive/3. Resources/Philosophy/Relationship/Relationship.md`
- `3. Resources/Philosophy/The Red Car Theory.md` → `archive/3. Resources/Philosophy/The Red Car Theory.md`
- `3. Resources/Philosophy/Thoughts.md` → `archive/3. Resources/Philosophy/Thoughts.md`
- `3. Resources/PodCast/Bella Vitta Podcast.md` → `archive/3. Resources/PodCast/Bella Vitta Podcast.md`
- `3. Resources/Tweets/Collection.md` → `archive/3. Resources/Tweets/Collection.md`
- `3. Resources/YouTube Video/Intro to Large Language Models Youtube Video.md` → `archive/3. Resources/YouTube Video/Intro to Large Language Models Youtube Video.md`
- `4. Archives/HaProxy Automation/HaProxy Automation.md` → `archive/4. Archives/HaProxy Automation/HaProxy Automation.md`
- `4. Archives/Income Proof 2023.md` → `archive/4. Archives/Income Proof 2023.md`
- `4. Archives/Karpenter/Setup Karpenter.md` → `archive/4. Archives/Karpenter/Setup Karpenter.md`
- `4. Archives/WorldCup Sales/Le Arch Word Cup.md` → `archive/4. Archives/WorldCup Sales/Le Arch Word Cup.md`
- `4. Archives/WorldCup Sales/Learnings.md` → `archive/4. Archives/WorldCup Sales/Learnings.md`
- `4. Archives/WorldCup Sales/Movies Arch World Cup.md` → `archive/4. Archives/WorldCup Sales/Movies Arch World Cup.md`
- `4. Archives/WorldCup Sales/WorldCup Prep.md` → `archive/4. Archives/WorldCup Sales/WorldCup Prep.md`
- `Assets/Untitled.md` → `archive/Assets/Untitled.md`
- `Journal/Daily Journal/2023-04-11.md` → `archive/Journal/Daily Journal/2023-04-11.md`
- `Journal/Daily Journal/2023-04-12.md` → `archive/Journal/Daily Journal/2023-04-12.md`
- `Journal/Daily Journal/2023-04-13.md` → `archive/Journal/Daily Journal/2023-04-13.md`
- `Journal/Daily Journal/2023-04-14.md` → `archive/Journal/Daily Journal/2023-04-14.md`
- `Journal/Daily Journal/2023-04-17.md` → `archive/Journal/Daily Journal/2023-04-17.md`
- `Journal/Daily Journal/2023-04-20.md` → `archive/Journal/Daily Journal/2023-04-20.md`
- `Journal/Daily Journal/2023-04-23.md` → `archive/Journal/Daily Journal/2023-04-23.md`
- `Journal/Daily Journal/2023-04-24.md` → `archive/Journal/Daily Journal/2023-04-24.md`
- `Journal/Daily Journal/2023-04-26.md` → `archive/Journal/Daily Journal/2023-04-26.md`
- `Journal/Daily Journal/2023-04-27.md` → `archive/Journal/Daily Journal/2023-04-27.md`
- `Journal/Daily Journal/2023-05-08.md` → `archive/Journal/Daily Journal/2023-05-08.md`
- `Journal/Daily Journal/2023-05-21.md` → `archive/Journal/Daily Journal/2023-05-21.md`
- `Journal/Daily Journal/2023-05-27.md` → `archive/Journal/Daily Journal/2023-05-27.md`
- `Journal/Daily Journal/2023-06-09.md` → `archive/Journal/Daily Journal/2023-06-09.md`
- `Journal/Daily Journal/2023-06-10.md` → `archive/Journal/Daily Journal/2023-06-10.md`
- `Journal/Daily Journal/2023-06-22.md` → `archive/Journal/Daily Journal/2023-06-22.md`
- `Journal/Daily Journal/2023-07-07.md` → `archive/Journal/Daily Journal/2023-07-07.md`
- `Journal/Daily Journal/2023-07-29.md` → `archive/Journal/Daily Journal/2023-07-29.md`
- `Journal/Daily Journal/2023-08-02.md` → `archive/Journal/Daily Journal/2023-08-02.md`
- `Journal/Daily Journal/2023-08-16.md` → `archive/Journal/Daily Journal/2023-08-16.md`
- `Journal/Daily Journal/2023-09-25.md` → `archive/Journal/Daily Journal/2023-09-25.md`
- `Journal/Daily Journal/2023-09-30.md` → `archive/Journal/Daily Journal/2023-09-30.md`
- `Journal/Daily Journal/2023-10-02.md` → `archive/Journal/Daily Journal/2023-10-02.md`
- `Journal/Daily Journal/2023-10-04.md` → `archive/Journal/Daily Journal/2023-10-04.md`
- `Journal/Daily Journal/2023-10-05.md` → `archive/Journal/Daily Journal/2023-10-05.md`
- `Journal/Daily Journal/2023-10-06.md` → `archive/Journal/Daily Journal/2023-10-06.md`
- `Journal/Daily Journal/2023-10-08.md` → `archive/Journal/Daily Journal/2023-10-08.md`
- `Journal/Daily Journal/2023-10-27.md` → `archive/Journal/Daily Journal/2023-10-27.md`
- `Journal/Daily Journal/2023-11-07.md` → `archive/Journal/Daily Journal/2023-11-07.md`
- `Journal/Daily Journal/2023-11-12.md` → `archive/Journal/Daily Journal/2023-11-12.md`
- `Journal/Daily Journal/2023-11-14.md` → `archive/Journal/Daily Journal/2023-11-14.md`
- `Journal/Daily Journal/2023-11-16.md` → `archive/Journal/Daily Journal/2023-11-16.md`
- `Journal/Daily Journal/2023-12-11.md` → `archive/Journal/Daily Journal/2023-12-11.md`
- `Journal/Daily Journal/2023-12-17.md` → `archive/Journal/Daily Journal/2023-12-17.md`
- `Journal/Daily Journal/2023-12-18.md` → `archive/Journal/Daily Journal/2023-12-18.md`
- `Journal/Daily Journal/2023-12-19.md` → `archive/Journal/Daily Journal/2023-12-19.md`
- `Journal/Daily Journal/2023-12-30.md` → `archive/Journal/Daily Journal/2023-12-30.md`
- `Journal/Daily Journal/2023-12-31.md` → `archive/Journal/Daily Journal/2023-12-31.md`
- `Journal/Daily Journal/2024-01-01.md` → `archive/Journal/Daily Journal/2024-01-01.md`
- `Journal/Daily Journal/2024-01-02.md` → `archive/Journal/Daily Journal/2024-01-02.md`
- `Journal/Daily Journal/2024-01-03.md` → `archive/Journal/Daily Journal/2024-01-03.md`
- `Journal/Daily Journal/2024-01-04.md` → `archive/Journal/Daily Journal/2024-01-04.md`
- `Journal/Daily Journal/2024-01-05.md` → `archive/Journal/Daily Journal/2024-01-05.md`
- `Journal/Daily Journal/2024-01-06.md` → `archive/Journal/Daily Journal/2024-01-06.md`
- `Journal/Daily Journal/2024-01-07.md` → `archive/Journal/Daily Journal/2024-01-07.md`
- `Journal/Daily Journal/2024-01-08.md` → `archive/Journal/Daily Journal/2024-01-08.md`
- `Journal/Daily Journal/2024-01-09.md` → `archive/Journal/Daily Journal/2024-01-09.md`
- `Journal/Daily Journal/2024-01-10.md` → `archive/Journal/Daily Journal/2024-01-10.md`
- `Journal/Daily Journal/2024-01-11.md` → `archive/Journal/Daily Journal/2024-01-11.md`
- `Journal/Daily Journal/2024-01-12.md` → `archive/Journal/Daily Journal/2024-01-12.md`
- `Journal/Daily Journal/2024-01-13.md` → `archive/Journal/Daily Journal/2024-01-13.md`
- `Journal/Daily Journal/2024-01-14.md` → `archive/Journal/Daily Journal/2024-01-14.md`
- `Journal/Daily Journal/2024-01-15.md` → `archive/Journal/Daily Journal/2024-01-15.md`
- `Journal/Daily Journal/2024-01-24.md` → `archive/Journal/Daily Journal/2024-01-24.md`
- `Journal/Daily Journal/2024-04-08.md` → `archive/Journal/Daily Journal/2024-04-08.md`
- `Journal/Daily Journal/2024-04-10.md` → `archive/Journal/Daily Journal/2024-04-10.md`
- `Journal/Daily Journal/2024-04-15.md` → `archive/Journal/Daily Journal/2024-04-15.md`
- `Journal/Daily Journal/2024-04-22.md` → `archive/Journal/Daily Journal/2024-04-22.md`
- `Journal/Daily Journal/2024-04-23.md` → `archive/Journal/Daily Journal/2024-04-23.md`
- `Journal/Daily Journal/2024-04-24.md` → `archive/Journal/Daily Journal/2024-04-24.md`
- `Journal/Daily Journal/2024-04-25.md` → `archive/Journal/Daily Journal/2024-04-25.md`
- `Journal/Daily Journal/2024-04-26.md` → `archive/Journal/Daily Journal/2024-04-26.md`
- `Journal/Daily Journal/2024-04-29.md` → `archive/Journal/Daily Journal/2024-04-29.md`
- `Journal/Daily Journal/2024-04-30.md` → `archive/Journal/Daily Journal/2024-04-30.md`
- `Journal/Daily Journal/2024-05-08.md` → `archive/Journal/Daily Journal/2024-05-08.md`
- `Journal/Daily Journal/2024-05-10.md` → `archive/Journal/Daily Journal/2024-05-10.md`
- `Journal/Daily Journal/2024-05-15.md` → `archive/Journal/Daily Journal/2024-05-15.md`
- `Journal/Daily Journal/2024-05-16.md` → `archive/Journal/Daily Journal/2024-05-16.md`
- `Journal/Daily Journal/2024-05-21.md` → `archive/Journal/Daily Journal/2024-05-21.md`
- `Journal/Daily Journal/2024-05-23.md` → `archive/Journal/Daily Journal/2024-05-23.md`
- `Journal/Daily Journal/2024-05-27.md` → `archive/Journal/Daily Journal/2024-05-27.md`
- `Journal/Daily Journal/2024-05-28.md` → `archive/Journal/Daily Journal/2024-05-28.md`
- `Journal/Daily Journal/2024-05-30.md` → `archive/Journal/Daily Journal/2024-05-30.md`
- `Journal/Daily Journal/2024-06-03.md` → `archive/Journal/Daily Journal/2024-06-03.md`
- `Journal/Daily Journal/2024-06-05.md` → `archive/Journal/Daily Journal/2024-06-05.md`
- `Journal/Daily Journal/2024-06-06.md` → `archive/Journal/Daily Journal/2024-06-06.md`
- `Journal/Daily Journal/2024-06-10.md` → `archive/Journal/Daily Journal/2024-06-10.md`
- `Journal/Daily Journal/2024-06-11.md` → `archive/Journal/Daily Journal/2024-06-11.md`
- `Journal/Daily Journal/2024-06-24 (conflict 2024-06-25-20-19-30).md` → `archive/Journal/Daily Journal/2024-06-24 (conflict 2024-06-25-20-19-30).md`
- `Journal/Daily Journal/2024-06-24 (conflict 2024-07-05-10-24-04).md` → `archive/Journal/Daily Journal/2024-06-24 (conflict 2024-07-05-10-24-04).md`
- `Journal/Daily Journal/2024-06-24.md` → `archive/Journal/Daily Journal/2024-06-24.md`
- `Journal/Daily Journal/2024-07-10.md` → `archive/Journal/Daily Journal/2024-07-10.md`
- `Journal/Daily Journal/2024-08-05.md` → `archive/Journal/Daily Journal/2024-08-05.md`
- `Journal/Daily Journal/2024-08-17.md` → `archive/Journal/Daily Journal/2024-08-17.md`
- `Journal/Daily Journal/2024-09-15.md` → `archive/Journal/Daily Journal/2024-09-15.md`
- `Journal/Daily Journal/2025-05-15.md` → `archive/Journal/Daily Journal/2025-05-15.md`
- `Journal/Daily Journal/Habit Tracker.md` → `archive/Journal/Daily Journal/Habit Tracker.md`
- `Journal/Weekly Journal/2024-W01.md` → `archive/Journal/Weekly Journal/2024-W01.md`
- `5 small habits Mel Robin Podcast.md` → `archive/loose/5 small habits Mel Robin Podcast.md`
- `AI Workshop.md` → `archive/loose/AI Workshop.md`
- `Archtects catup 27-05.md` → `archive/loose/Archtects catup 27-05.md`
- `Body Language Venessa Podcast.md` → `archive/loose/Body Language Venessa Podcast.md`
- `Cold Play.md` → `archive/loose/Cold Play.md`
- `ColdPlay Load Handling.md` → `archive/loose/ColdPlay Load Handling.md`
- `EBS - Millions-of-tiny-databases.md` → `archive/loose/EBS - Millions-of-tiny-databases.md`
- `Entrepreneurship masterclass Ali Abdaal.md` → `archive/loose/Entrepreneurship masterclass Ali Abdaal.md`
- `Epics for DR.md` → `archive/loose/Epics for DR.md`
- `Exit Strategy.md` → `archive/loose/Exit Strategy.md`
- `Framing Bias.md` → `archive/loose/Framing Bias.md`
- `Go Lang Talk - BookmyShow.md` → `archive/loose/Go Lang Talk - BookmyShow.md`
- `HaProxy changes.md` → `archive/loose/HaProxy changes.md`
- `Home Dashboard.md` → `archive/loose/Home Dashboard.md`
- `Idea Generation.md` → `archive/loose/Idea Generation.md`
- `Ideas for business.md` → `archive/loose/Ideas for business.md`
- `Learning from ColdPlay.md` → `archive/loose/Learning from ColdPlay.md`
- `Load Test Results..md` → `archive/loose/Load Test Results..md`
- `Making of a Manager.md` → `archive/loose/Making of a Manager.md`
- `Million dollar weekend Noah keagen Podcast.md` → `archive/loose/Million dollar weekend Noah keagen Podcast.md`
- `MQTT vs HTTP.md` → `archive/loose/MQTT vs HTTP.md`
- `Negotiation Technique.md` → `archive/loose/Negotiation Technique.md`
- `Optimise Prometheus Resources.md` → `archive/loose/Optimise Prometheus Resources.md`
- `Ozone.md` → `archive/loose/Ozone.md`
- `PCI DSS 2024-25.md` → `archive/loose/PCI DSS 2024-25.md`
- `Pre Req for Load Testing.md` → `archive/loose/Pre Req for Load Testing.md`
- `Questions for AWS EBS team.md` → `archive/loose/Questions for AWS EBS team.md`
- `Renewable Energy.md` → `archive/loose/Renewable Energy.md`
- `Semi Conductor Industry.md` → `archive/loose/Semi Conductor Industry.md`
- `Shoe Company.md` → `archive/loose/Shoe Company.md`
- `Solar industry.md` → `archive/loose/Solar industry.md`
- `Space of the Retailer.md` → `archive/loose/Space of the Retailer.md`
- `SRE KRAs and Roles.md` → `archive/loose/SRE KRAs and Roles.md`
- `SRE Make things better 09-05-2024.md` → `archive/loose/SRE Make things better 09-05-2024.md`
- `stocks.md` → `archive/loose/stocks.md`
- `Strategy for EKS and ECS.md` → `archive/loose/Strategy for EKS and ECS.md`
- `System Design Interview An Insiders Guide.md` → `archive/loose/System Design Interview An Insiders Guide.md`
- `Technical Analysis.md` → `archive/loose/Technical Analysis.md`
- `The almanak of naval ravikant.md` → `archive/loose/The almanak of naval ravikant.md`
- `Thridparty Automation Project.md` → `archive/loose/Thridparty Automation Project.md`
- `Untitled 2.md` → `archive/loose/Untitled 2.md`
- `Untitled 5.md` → `archive/loose/Untitled 5.md`
- `Untitled.md` → `archive/loose/Untitled.md`
- `VM Ware Debugging.md` → `archive/loose/VM Ware Debugging.md`
- `Meeting Notes/AB Testing.md` → `archive/Meeting Notes/AB Testing.md`
- `Meeting Notes/Cost Optimisation Exercise.md` → `archive/Meeting Notes/Cost Optimisation Exercise.md`
- `Meeting Notes/DevOps Sre Suggestions.md` → `archive/Meeting Notes/DevOps Sre Suggestions.md`
- `Meeting Notes/LK Migration Cutover.md` → `archive/Meeting Notes/LK Migration Cutover.md`
- `Meeting Notes/SRE GuideLines.md` → `archive/Meeting Notes/SRE GuideLines.md`
- `Meeting Notes/White Labeling Discussion.md` → `archive/Meeting Notes/White Labeling Discussion.md`

## Trashed

None. Nothing was deleted or moved to `.trash/` in this migration.

## Verification

- Pre-move total enumerated: 377 (377 - 1 for `Home.md` which stays at root = 376 moved)
- Post-move: 63 in `sources/learning/books/` + 313 in `archive/` = 376 ✓
- Remaining at vault root: `CLAUDE.md`, `Home.md`, `wiki/`, `output/`, `sources/`, `archive/`, `Templates/`, `.claude/`, `.obsidian/`, `.trash/`

## Recovery

All archived content is reversible — simply `mv` from `archive/` back to its original location if a decision needs undoing. Nothing was deleted.
