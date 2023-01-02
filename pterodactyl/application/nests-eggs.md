### Example Model (nests)

```json
{
  "author": "support@pterodactyl.io",
  "created_at": "2022-01-03T08:07:20+00:00",
  "description": "Minecraft - the classic game from Mojang. With support for Vanilla MC, Spigot, and many others!",
  "id": 1,
  "name": "Minecraft",
  "updated_at": "2022-01-03T08:07:20+00:00",
  "uuid": "535d963e-9eed-4145-8f10-151cf625211e"
}
```

### `GET /nests`

Returns a list of nest objects.

### Parameters

| Name     | Supported | Allowed Values |
| -------- | --------- | -------------- |
| filter   | ❌        |
| include  | ✅        | eggs, servers  |
| sort     | ❌        |
| page     | ✅        | Any number     |
| per_page | ✅        | Any number     |

### `GET /nests/:id`

Returns a nest by its `id` (number). Supports the above parameters.

### Example Model (eggs)

```json
{
  "author": "support@pterodactyl.io",
  "config": {
    "extends": null,
    "file_denylist": [],
    "files": {
      "config.yml": {
        "find": {
          "listeners[0].host": "0.0.0.0:{{server.build.default.port}}",
          "listeners[0].query_port": "{{server.build.default.port}}",
          "servers.*.address": {
            "regex:^(127\\.0\\.0\\.1|localhost)(:\\d{1,5})?$": "{{config.docker.interface}}$2"
          }
        },
        "parser": "yaml"
      }
    },
    "logs": [],
    "startup": {
      "done": "Listening on "
    },
    "stop": "end"
  },
  "created_at": "2022-01-03T08:07:20+00:00",
  "description": "For a long time, Minecraft server owners have had a dream that encompasses a free, easy, and reliable way to connect multiple Minecraft servers together. BungeeCord is the answer to said dream. Whether you are a small server wishing to string multiple game-modes together, or the owner of the ShotBow Network, BungeeCord is the ideal solution for you. With the help of BungeeCord, you will be able to unlock your community's full potential.",
  "docker_image": "ghcr.io/pterodactyl/yolks:java_17",
  "docker_images": {
    "Java 11": "ghcr.io/pterodactyl/yolks:java_11",
    "Java 16": "ghcr.io/pterodactyl/yolks:java_16",
    "Java 17": "ghcr.io/pterodactyl/yolks:java_17",
    "Java 8": "ghcr.io/pterodactyl/yolks:java_8"
  },
  "id": 1,
  "name": "Bungeecord",
  "nest": 1,
  "script": {
    "container": "ghcr.io/pterodactyl/installers:alpine",
    "entry": "ash",
    "extends": null,
    "install": "#!/bin/ash\r\n# Bungeecord Installation Script\r\n#\r\n# Server Files: /mnt/server\r\n\r\ncd /mnt/server\r\n\r\nif [ -z \"${BUNGEE_VERSION}\" ] || [ \"${BUNGEE_VERSION}\" == \"latest\" ]; then\r\n    BUNGEE_VERSION=\"lastStableBuild\"\r\nfi\r\n\r\ncurl -o ${SERVER_JARFILE} https://ci.md-5.net/job/BungeeCord/${BUNGEE_VERSION}/artifact/bootstrap/target/BungeeCord.jar",
    "privileged": true
  },
  "startup": "java -Xms128M -XX:MaxRAMPercentage=95.0 -jar {{SERVER_JARFILE}}",
  "updated_at": "2022-06-27T03:53:00+00:00",
  "uuid": "ebd6956d-e9d2-4a67-bd23-c0abd5cd3dfc"
}
```

### `GET /nests/:id/eggs`

Returns a list of eggs in the nest.

### Parameters

| Name     | Supported | Allowed Values                           |
| -------- | --------- | ---------------------------------------- |
| filter   | ❌        |
| include  | ✅        | config, nest, script, servers, variables |
| sort     | ❌        |
| page     | ✅        | Any number                               |
| per_page | ✅        | Any number                               |

### `GET /nests/:id/eggs/:id`

Returns an egg in a nest by its `id` (number). Supports the above parameters.
