# BeautyMApp for Clinics

An interactive prototype of the **B2B side** of BeautyMApp: the console a partner clinic logs into to receive and work the qualified leads the consumer app sends them.

> **Prototype.** All data is illustrative. No real patient records, no backend, no persistence.

---

## What this is

BeautyMApp is an AI-powered beauty and skin-tech platform. A user photographs their face, gets an AI skin analysis, sees a simulated "after" result, and receives personalised treatment recommendations. When they tap **Book a consultation**, that request has to land somewhere.

This is where it lands.

The consumer app already exists as a separate demo. This repository covers the half that had never been built - the screen a clinic stares at, and the part of the product clinics actually pay for.

**Why a clinic pays:** a normal enquiry is someone who filled in a form. A BeautyMApp lead arrives with the skin analysis done, the treatment identified, the budget stated, and the user having already seen a simulation of the result. Far more of them book.

---

## Screens

| Screen | What it does |
| --- | --- |
| **Leads** | The pipeline. Every consultation request, how long it has been waiting, and its status. |
| **Performance** | Revenue attributed, average treatment value, cost per booked lead vs. paid social, return on spend, and which treatments convert. |
| **Treatment catalogue** | The 19 treatments this clinic offers. Pause one and those leads route elsewhere. |
| **Availability** | A weekly slot grid. A reach meter shows what share of nearby users your open hours can match. |
| **Settings** | Clinic profile, matching rules (radius, price band, lead cap, auto-accept), notifications, theme. |

### Lead detail

Selecting a lead opens a panel containing:

- **AI skin analysis** - concerns with severity
- **The simulation the user saw**, with an illustrative-only disclaimer
- **Ranked treatment recommendations** - selectable, so the clinic chooses which one it proposes
- **Why this lead was matched here** - treatment offered, distance, price band, availability, rating, case history
- **User preferences** - budget, availability, travel radius, previous treatments
- **Status controls** - New → Contacted → Booked → Completed

Moving a lead through the pipeline recalculates the stat tiles, filter counts and conversion funnel live.

---

## Running it

Open `index.html`. That's the whole thing.

No build step, no dependencies, no server, no internet connection. One self-contained file - HTML, CSS and JavaScript inline, favicon embedded as a data URI.

To deploy, drop the folder into Netlify, Vercel, or GitHub Pages.

---

## Design

Built to BeautyMApp's brand board - deep plum `#4A3348`, dusty rose `#B8788C`, warm ivory ground.

- **Themes** - light and dark, following the operating system, with a manual override in the top bar and in Settings. The choice persists.
- **Mobile** - the sidebar is replaced by a floating bottom tab bar. Tables become cards. Metrics and filters scroll horizontally rather than wrapping.
- **Accessibility** - keyboard navigable, visible focus states, ARIA roles on menus, switches and dialogs, and `prefers-reduced-motion` respected.

---

## Changing the data

Everything lives in plain arrays near the bottom of `index.html`:

| Array | Holds |
| --- | --- |
| `LEADS` | The 16 consultation requests - names, cities, concerns, recommendations, match reasoning, preferences |
| `TREATMENTS` | The treatment catalogue |
| `WEEKS` / `CONVERT` | Chart data |
| `WEIGHT` | How much each availability block widens your match pool |

Currency, city names and treatment prices are all in `LEADS` and `TREATMENTS`. Swapping market means editing those two arrays and nothing else.

**Current assumption:** a Belgrade clinic, prices in euros. Serbia's currency is the dinar, though aesthetic clinics there commonly quote in euros. If the launch market is the US, both arrays need swapping.

---

## Not built

Deliberately left out, because faking them would mislead rather than demonstrate:

- **Multi-location clinic switching** - worth building properly; every branch would otherwise show identical leads
- **Messaging** - depends on whether clinics reply in-platform or by their own phone and email
- **Export, billing, team management** - stubbed with honest "not built yet" messages
- **Persistence** - status changes reset on reload

---

## Open questions for the product

1. Which treatments do partner clinics actually offer, and at what prices?
2. How should clinic matching work - what genuinely decides routing?
3. What does the consumer app capture when a user requests a consultation?
4. Do clinics reply inside the platform, or through their own channels?
5. Which market launches first? It sets currency, names and regulation.

---

## Notes on compliance

Two things were built in rather than added later, because clinics operating in the EU will ask:

- **Surnames are masked** until a clinic accepts a request. Contact details are released on acceptance.
- **Simulated results carry an explicit disclaimer** that they are illustrative and not a medical diagnosis, and that a qualified clinician confirms suitability at consultation.

Neither is sufficient for real GDPR or medical-device compliance. Both signal that the product was designed with them in mind.
