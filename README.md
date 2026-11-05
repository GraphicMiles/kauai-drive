# Kauaʻi Drive

A stylised open-world island you can drive around: a closed coast road, a
switchback mountain pass, jungle tracks, an ancient heiau and a steel arch bridge
over a gorge. Stay on the asphalt or leave it anywhere, including into the sea.

The client is one self-contained HTML file with the renderer inlined. A small
Node and WebSocket server hosts it and runs the lobby for online racing.

## Why it exists

Driving games usually trade freedom for content: a big map, or a good car. This
is an attempt at the smallest honest version of both, where the island is small
enough to hand-build and large enough that you can get lost, and where the car
feels like it has weight because the physics are real rather than animated.

## What you can do

- **Free drive** anywhere on the island: asphalt, dunes, jungle, lava rock or
  the sea.
- **Race three laps** through the orange beacons, alone or against someone else
  in the same lobby.
- **Drive a car with four spring-damper wheels** rather than a fixed camera on
  rails, so the body rolls, squats and recovers.
- **Look at the palms.** Every palm on the island is procedural: a leaning
  S-curve trunk, leaf scars, a flared root mass and fronds on golden-angle
  phyllotaxis, at one of four detail levels.
- **Drive it on a phone**, where the same build serves touch controls.

## Running it

```bash
npm ci
npm start
```

Then open http://localhost:3000. The same Node process serves `public/` and the
WebSocket endpoint.

## What is not here

- There is no career, no upgrade system and no traffic. The race is three laps.
- Online play is a lobby and a position relay, not an authoritative server. Two
  players with bad connections will see each other stutter.
- The island is hand-authored, so it does not extend past its coast.
- A free Render instance sleeps after about fifteen minutes of inactivity and
  wakes on the next request.

## How it is built

```
public/index.html        the whole client, renderer inlined
public/palm-tree.js      the procedural palm used across the island
server.js                static host plus WebSocket relay and lobby
test/                    multiplayer flow, palm and palm field tests
tools/check-html.js      structural check on the single-file client
render.yaml              Render blueprint
```

Nothing is fetched from a CDN: there are no model or texture downloads, and the
renderer ships inside the HTML file.

### Tests

```bash
npm test              # multiplayer flow
npm run test:palm     # procedural palm geometry
npm run test:palm-field
npm run test:html     # checks the single-file client
npm run probe:scene   # scene inspection
```

### Deploy

The Node process serves both the static client and the WebSocket endpoint, so a
single host is enough. `render.yaml` is the blueprint used; set `PORT` in the
environment.

## Licence

MIT, see `LICENSE`.
