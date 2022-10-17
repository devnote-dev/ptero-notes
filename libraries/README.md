# API Wrappers/Libraries
Below is a list of curated API wrappers and libraries for Pterodactyl maintained by official Pterodactyl staff and/or volunteers in the community.

Name                                                            | Language(s)   | Supports
----------------------------------------------------------------|---------------|-------------------------------
[Bash-PteroAPI](https://github.com/Silent-dawn/bash-pteroapi)   | Bash          | Client
[Crocgodyl](https://github.com/parkervcp/crocgodyl)             | Go            | Application, Client
[Dartactyl](https://github.com/TekExplorer/dartactyl)           | Dart          | Client, Websocket
[Elidactyl](https://github.com/kintu-games/elidactyl)           | Elixir        | Application
[Nodeactyl](https://github.com/Nodeactyl/Nodeactyl)             | JS            | Application, Client
[Pterodcatyl4J](https://github.com/mattmalec/Pterodactyl4J)     | Java, Kotlin  | Application, Client, Websocket
[PteroJS](https://github.com/PteroPackages/PteroJS)             | JS, TS        | Application, Client, Websocket
[Pydactyl](https://github.com/iamkubi/pydactyl)                 | Python        | Application, Client

## Supports Scopes

Name | Minimum Coverage | Additional Coverage
-----|------------------|--------------------
Application | users, servers, nodes | locations, nests, eggs
Client | account (2FA, email & password, API keys), servers (resources, command, power) | account (activity, SSH keys), servers (activity), databases, files schedules, network, users (subusers), backups, startup, settings
Websocket | connect, heartbeat, receive events | send events
