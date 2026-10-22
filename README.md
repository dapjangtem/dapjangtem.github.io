# dapjangtem.github.io

## Counters

Page loads, affiliate-link clicks, and search submits are counted with the free [Abacus](https://abacus.jasoncameron.dev) API (namespace `dapjangtem`). The page does not show the counts. No cookies and no personal data are sent. If Abacus is unreachable, the page behaves as before.

Abacus keys and namespaces must match `^[A-Za-z0-9_.-]{3,64}$`. These calls use the documented endpoints:

- Increment: `GET https://abacus.jasoncameron.dev/hit/dapjangtem/<key>`
- Read without incrementing: `GET https://abacus.jasoncameron.dev/get/dapjangtem/<key>`

A read returns `{ "value": 123 }`. A key that has never been hit returns `404`.

| Key | Counts |
| --- | --- |
| `visits` | Page loads |
| `search` | Search submits (Enter in the episode search box) |
| `click-ep3` | Clicks on the EP3 link |
| `click-t1` | Clicks on the T1 link |
| `click-ep2` | Clicks on the EP2 link |
| `click-ep1` | Clicks on the EP1 link |

A new `LINKS` row is counted as `click-` plus its `ep` in lowercase (`EP4` → `click-ep4`). Clicks are sent with `fetch` and `keepalive` so navigation is not delayed. `navigator.sendBeacon` is not used: Abacus only increments `GET /hit/...`, and a POST is redirected without counting.