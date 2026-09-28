[简体中文](README.md) | [繁體中文](README.zh-TW.md) | [English](README.en.md)

# Online Texas Hold'em Platform Source Code

This repository exposes selected C++ game-server components, Tars protocols, room/client message handlers and real product screens for an **online Texas Hold'em platform**. It is useful for studying multiplayer hand state, betting messages, room synchronization, private tables and club-oriented product flows.

> Scope: code-verified behavior and screenshot-demonstrated product entry points are described separately. The public tree does not include Docker Compose, database initialization scripts or benchmark reports, so it should not be presented as verified one-click production deployment.

## Player-facing product journey

1. **Account entry**: phone/email login, registration and password recovery are visible in the product UI.
2. **Lobby and filters**: the lobby shows Hold'em, AOF, 6+ Short Deck, MTT and SNG entries with blinds, duration and seat counts.
3. **Private table creation**: configure mode, blinds, 60–180 minutes, 2–9 players and speed.
4. **Club flow**: create or join by club ID and browse joined clubs with table counts.
5. **Live table**: seats, pot, community cards, hole cards, fold, check and raise controls.
6. **Player profile**: VIP, inventory, achievements, game statistics, support and settings.

## Real product screens

| Account entry | Lobby and modes |
| --- | --- |
| ![Online Texas Holdem phone and email login](docs/assets/screenshots/001.jpg) | ![Holdem AOF Short Deck MTT and SNG lobby](docs/assets/screenshots/1111.jpg) |
| Private table setup | Club list |
| ![Private poker table mode blinds duration and seats](docs/assets/screenshots/2222.jpg) | ![Texas Holdem club list and table counts](docs/assets/screenshots/3333.jpg) |
| Player profile | Real-time table |
| ![Poker player profile and statistics](docs/assets/screenshots/4444.jpg) | ![Multiplayer real-time Texas Holdem table](docs/assets/screenshots/5555.jpg) |

[Open the illustrated English product page](https://deeptexas-ai.github.io/online-holdem-platform/)

## Code-verified technical modules

| Module | Main files | Verifiable scope |
| --- | --- | --- |
| Game state machine | `process/process.cpp`, `process/process.h` | Begin, ante, banker, hole cards, community cards, turn, river and game end transitions |
| Table recovery | `gamestation.cpp` | Phase, player state, bets, community cards, hole-card visibility and remaining action time |
| Message handling | `message/`, `onclientmessage.*`, `onroommessage.*` | Client/room messages and delivery to one player, all players or watchers |
| Hold'em protocol | `protos/dzproto.tars` | Blinds, minimum buy-in, actions, pot, cards, records, auto bet, buy-in and timer messages |
| Game service | `gameserver.*`, `gameroot.*` | Room/game communication, broadcasts and the game root object |
| Push interface | `PushServant.tars`, `PushServer.h` | Push service interface and server entry |

## Product boundary

- The code directly demonstrates blinds, hole/community cards, turn/river, actions, pot, buy-in, records and game-end flow.
- Screens demonstrate Hold'em, AOF, 6+ Short Deck, MTT, SNG, private rooms and clubs.
- Complete rules for every extension, tournament scheduling, payments, database, admin panel, voice and production dependencies require separate acceptance testing.

## Contact

- Telegram: [@xuzongbin001](https://t.me/xuzongbin001)
- Email: [masterai918@gmail.com](mailto:masterai918@gmail.com)

Follow applicable laws, platform policies, privacy and minor-protection requirements. Do not use this project for illegal gambling.
