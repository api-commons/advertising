# Advertising

The common advertising vocabulary -- the ad accounts that pay, the campaigns they run, the ad groups that target and budget within them, the ads and creatives that run, the audiences they reach and the performance reported back -- distilled from the APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Advertising, AdTech, Ad Tech, Programmatic, Programmatic Advertising, Digital Advertising, Performance Marketing, Ad Network, Retail Media in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| ad_account | 25 | 23 | name 52% | advertisers 14, advertiser 7, ad-accounts 3, accounts 2 |
| ad_campaign | 16 | 16 | name 88%, id 69%, account_id 62%, status 62%, budget 50%, campaign_id 50%, created_at 50%, end_date 50%, start_date 50%, updated_at 50% | campaigns 15, campaign 4, ad-campaigns 1 |
| ad_group | 16 | 16 | id 88%, name 75%, campaign_id 69% | adgroups 4, ad-groups 4, lineitems 3, ad_groups 3 |
| ad | 7 | 7 | id 86%, name 71%, creative_id 57% | ads 7, ad 1 |
| creative | 10 | 9 | id 100%, name 100%, type 78% | creatives 9, adcreatives 1, creative 1 |
| ad_audience | 9 | 9 | name 56% | audiences 7, audience 2, customaudiences 1, custom_audiences 1 |
| ad_report | 9 | 8 | id 50% | reports 6, report 4, insights 3, performance 1 |

Cohort: 134 providers with harvested OpenAPI, 33 crosswalks. Of the providers exposing a ad_account: 56% create, 80% list, 56% fetch, 24% update, 16% delete. Generated 2026-11-10 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- An ad campaign agrees more than anything else in advertising: name, status, account, budget, start and end dates are all core. The campaign is where ad platforms converged.
- An ad group agrees on id, name and its campaign -- the hierarchy is shared even where the targeting inside it is not. Meta's ad sets, DV360's line items and Amazon's ad groups are one concept.
- Reports agree only on an id: every platform reports impressions, clicks and spend, under its own names and its own breakdowns.
- Ads themselves are thin as a resource (7 providers); most platforms expose the ad through its creative.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- Ad campaigns are `/ad-campaigns` and audiences `/ad-audiences`, though ad platforms say `campaigns` and `audiences`: email marketing uses both words for something else. Reports are `/ad-reports` for the same reason.
- An ad group covers ad sets, line items, insertion orders and ad squads: the level beneath a campaign that carries budget and targeting.
- Ad-intelligence tools that list other companies' advertisers are not ad accounts.
- Duplicates merged: Habu into LiveRamp, Rubicon Project into Magnite, Mavrck into Later, Gist into ProRata.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
