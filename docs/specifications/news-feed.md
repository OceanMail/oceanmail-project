# OceanMail News Feed — Preliminary Product/Architecture Direction

Status: **CURRENT DIRECTION; NOT IMPLEMENTATION-READY**

## Purpose

Preserve the accepted direction for a very-low-bandwidth OceanMail news service without turning early exploration into an implementation contract.

The feature is intended to make selected news and public-information content useful over constrained OceanMail links by reducing source material to compact text-oriented content that can be cached and redistributed efficiently.

## Settled direction

- OceanMail will **not** attempt to mirror or cache every news article on the public Internet.
- News ingestion is **curated and bounded**: start with a small number of explicitly selected sources rather than arbitrary user-entered web crawling or global feed mirroring.
- RSS/Atom is the preferred initial ingest mechanism where a selected source provides it.
- Server-side processing should normalize selected feed content toward a text-first representation, removing presentation-only HTML and other nonessential web payload.
- Normalized news content is intended to be compressed and cached for later OceanMail distribution rather than repeatedly transferring the original web representation.
- The future Grid may distribute/cache eligible news content beyond the origin Server, but this does **not** authorize speculative global mesh behavior or override the existing evidence-gated relay/routing architecture.

## Component boundary

### Server

The hosted Server is the natural ownership boundary for Internet-side source acquisition, feed polling, normalization, source policy, provenance metadata, and any rights/retention rules that depend on the original publisher or feed.

### Station / Grid

Station/Grid behavior may later advertise, request, cache, relay, expire, or evict normalized news objects according to accepted Grid, storage, scheduling, and resource policies. News caching must not be used as a reason to duplicate authoritative mail payload queues or to bypass current Station STORE / TRANSPORT and GRID / CONTROL boundaries.

### Desktop / future clients

Presentation, subscription, article-selection, and progressive retrieval UX remain client/product design work and are not specified here.

## Not yet settled

The following remain unresolved and must not be inferred from this document:

- the initial source or sources;
- whether a source supplies full article text, summaries, or headline-only feed entries;
- whether OceanMail may fetch linked web pages when a feed contains only excerpts;
- publisher terms, copyright, redistribution rights, licensing, attribution, and retention requirements;
- whether OceanMail distributes headlines, summaries, full text, or multiple progressive tiers;
- the normalized article/object schema, identifiers, hashes, signatures, and provenance fields;
- cache TTLs, size limits, regional replication, popularity rules, subscription rules, and eviction behavior;
- how manifests/catalogs are represented or synchronized;
- whether news is modeled as a distinct Grid content object, a service object, or another existing transport-compatible form;
- scheduling/accounting treatment relative to mail, control traffic, firmware/background data, and Emergency traffic;
- exact compression format and measured compression ratio for representative news text;
- production throughput or transfer-time expectations.

## Performance evidence rule

No compression ratio or transfer-time estimate from exploratory chat is accepted as project evidence. Before capacity planning, benchmark a representative normalized news corpus through the currently accepted compression/store-transport path and report actual compressed sizes plus protocol overhead.

## Legal/source rule

The existence of an RSS/Atom feed does not by itself establish a right to redistribute full article text. Source selection and extraction behavior must be reviewed source-by-source before production redistribution. Public-domain or clearly licensed sources may be easier initial candidates, but no source is selected by this document.

## Implementation gate

Do not implement broad feed crawling, global article replication, or full-text redistribution solely from this preliminary direction. First settle source rights, object/manifest semantics, cache policy, and the narrow Server/Station contract required by the first testable slice.
