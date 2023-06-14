### `GET /api/remote/servers/:uuid`

Returns details about the server that allows Wings to self-recover and ensure that the state of the server matches the Panel at all times.

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 200  | The request was successful. |
| 404  | The server was not found.   |

### Response example

```json
{
  "settings": {
    "uuid": "1abc23d4-567e-8f9g-9h01-2ij34k56lmno",
    "meta": {
      "name": "My server",
      "description": ""
    },
    "suspended": false,
    "environment": {
      "SERVER_JARFILE": "server.jar",
      "MC_VERSION": "latest",
      "BUILD_TYPE": "recommended",
      "FORGE_VERSION": "",
      "STARTUP": "java -Xms128M -XX:MaxRAMPercentage=95.0 -Dterminal.jline=false -Dterminal.ansi=true $( [[  ! -f unix_args.txt ]] && printf %s \"-jar {{SERVER_JARFILE}}\" || printf %s \"@unix_args.txt\" )",
      "P_SERVER_LOCATION": "home",
      "P_SERVER_UUID": "1abc23d4-567e-8f9g-9h01-2ij34k56lmno",
      "P_SERVER_ALLOCATION_LIMIT": 0
    },
    "invocation": "java -Xms128M -XX:MaxRAMPercentage=95.0 -Dterminal.jline=false -Dterminal.ansi=true $( [[  ! -f unix_args.txt ]] && printf %s \"-jar {{SERVER_JARFILE}}\" || printf %s \"@unix_args.txt\" )",
    "skip_egg_scripts": false,
    "build": {
      "memory_limit": 0,
      "swap": 0,
      "io_weight": 500,
      "cpu_limit": 0,
      "threads": null,
      "disk_space": 0,
      "oom_disabled": true
    },
    "container": {
      "image": "ghcr.io/pterodactyl/yolks:java_8",
      "oom_disabled": true,
      "requires_rebuild": false
    },
    "allocations": {
      "force_outgoing_ip": false,
      "default": {
        "ip": "127.0.0.1",
        "port": 25565
      },
      "mappings": {
        "127.0.0.1": [
          25565
        ]
      }
    },
    "mounts": [],
    "egg": {
      "id": "a1b2c3d4-5ef6-7g8h-9012-34i5j67k8l9m",
      "file_denylist": []
    }
  },
  "process_configuration": {
    "startup": {
      "done": [
        ")! For help, type "
      ],
      "user_interaction": [],
      "strip_ansi": false
    },
    "stop": {
      "type": "command",
      "value": "stop"
    },
    "configs": [
      {
        "parser": "properties",
        "file": "server.properties",
        "replace": [
          {
            "match": "server-ip",
            "replace_with": "0.0.0.0"
          },
          {
            "match": "server-port",
            "replace_with": "25565"
          },
          {
            "match": "query.port",
            "replace_with": "25565"
          }
        ]
      }
    ]
  }
}
```

Sources

- [app/Http/Controllers/Api/Remote/Servers/ServerDetailsController.php#L35](https://github.com/pterodactyl/panel/blob/v1.11.3/app/Http/Controllers/Api/Remote/Servers/ServerDetailsController.php#L35)

---

### `GET /api/remote/servers/:uuid/install`

Returns installation information for a server.

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 200  | The request was successful. |
| 404  | The server was not found.   |

### Response example

```json
{
  "body": {
    "container_image": "openjdk:8-jdk-slim",
    "entrypoint": "bash",
    "script": "#!/bin/bash\r\n# Forge Installation Script\r\n#\r\n# Server Files: /mnt/server\r\napt update\r\napt install -y curl jq\r\n\r\nif [[ ! -d /mnt/server ]]; then\r\n  mkdir /mnt/server\r\nfi\r\n\r\ncd /mnt/server\r\n\r\n# Remove spaces from the version number to avoid issues with curl\r\nFORGE_VERSION=\"$(echo \"$FORGE_VERSION\" | tr -d ' ')\"\r\nMC_VERSION=\"$(echo \"$MC_VERSION\" | tr -d ' ')\"\r\n\r\nif [[ ! -z ${FORGE_VERSION} ]]; then\r\n  DOWNLOAD_LINK=https://maven.minecraftforge.net/net/minecraftforge/forge/${FORGE_VERSION}/forge-${FORGE_VERSION}\r\n  FORGE_JAR=forge-${FORGE_VERSION}*.jar\r\nelse\r\n  JSON_DATA=$(curl -sSL https://files.minecraftforge.net/maven/net/minecraftforge/forge/promotions_slim.json)\r\n\r\n  if [[ \"${MC_VERSION}\" == \"latest\" ]] || [[ \"${MC_VERSION}\" == \"\" ]]; then\r\n    echo -e \"getting latest version of forge.\"\r\n    MC_VERSION=$(echo -e ${JSON_DATA} | jq -r '.promos | del(.\"latest-1.7.10\") | del(.\"1.7.10-latest-1.7.10\") | to_entries[] | .key | select(contains(\"latest\")) | split(\"-\")[0]' | sort -t. -k 1,1n -k 2,2n -k 3,3n -k 4,4n | tail -1)\r\n    BUILD_TYPE=latest\r\n  fi\r\n\r\n  if [[ \"${BUILD_TYPE}\" != \"recommended\" ]] && [[ \"${BUILD_TYPE}\" != \"latest\" ]]; then\r\n    BUILD_TYPE=recommended\r\n  fi\r\n\r\n  echo -e \"minecraft version: ${MC_VERSION}\"\r\n  echo -e \"build type: ${BUILD_TYPE}\"\r\n\r\n  ## some variables for getting versions and things\r\n  FILE_SITE=https://maven.minecraftforge.net/net/minecraftforge/forge/\r\n  VERSION_KEY=$(echo -e ${JSON_DATA} | jq -r --arg MC_VERSION \"${MC_VERSION}\" --arg BUILD_TYPE \"${BUILD_TYPE}\" '.promos | del(.\"latest-1.7.10\") | del(.\"1.7.10-latest-1.7.10\") | to_entries[] | .key | select(contains($MC_VERSION)) | select(contains($BUILD_TYPE))')\r\n\r\n  ## locating the forge version\r\n  if [[ \"${VERSION_KEY}\" == \"\" ]] && [[ \"${BUILD_TYPE}\" == \"recommended\" ]]; then\r\n    echo -e \"dropping back to latest from recommended due to there not being a recommended version of forge for the mc version requested.\"\r\n    VERSION_KEY=$(echo -e ${JSON_DATA} | jq -r --arg MC_VERSION \"${MC_VERSION}\" '.promos | del(.\"latest-1.7.10\") | del(.\"1.7.10-latest-1.7.10\") | to_entries[] | .key | select(contains($MC_VERSION)) | select(contains(\"latest\"))')\r\n  fi\r\n\r\n  ## Error if the mc version set wasn't valid.\r\n  if [ \"${VERSION_KEY}\" == \"\" ] || [ \"${VERSION_KEY}\" == \"null\" ]; then\r\n    echo -e \"The install failed because there is no valid version of forge for the version of minecraft selected.\"\r\n    exit 1\r\n  fi\r\n\r\n  FORGE_VERSION=$(echo -e ${JSON_DATA} | jq -r --arg VERSION_KEY \"$VERSION_KEY\" '.promos | .[$VERSION_KEY]')\r\n\r\n  if [[ \"${MC_VERSION}\" == \"1.7.10\" ]] || [[ \"${MC_VERSION}\" == \"1.8.9\" ]]; then\r\n    DOWNLOAD_LINK=${FILE_SITE}${MC_VERSION}-${FORGE_VERSION}-${MC_VERSION}/forge-${MC_VERSION}-${FORGE_VERSION}-${MC_VERSION}\r\n    FORGE_JAR=forge-${MC_VERSION}-${FORGE_VERSION}-${MC_VERSION}.jar\r\n    if [[ \"${MC_VERSION}\" == \"1.7.10\" ]]; then\r\n      FORGE_JAR=forge-${MC_VERSION}-${FORGE_VERSION}-${MC_VERSION}-universal.jar\r\n    fi\r\n  else\r\n    DOWNLOAD_LINK=${FILE_SITE}${MC_VERSION}-${FORGE_VERSION}/forge-${MC_VERSION}-${FORGE_VERSION}\r\n    FORGE_JAR=forge-${MC_VERSION}-${FORGE_VERSION}.jar\r\n  fi\r\nfi\r\n\r\n#Adding .jar when not eding by SERVER_JARFILE\r\nif [[ ! $SERV\njava -jar installer.jar --installServer || { echo -e \"\\nInstall failed using Forge version ${FORGE_VERSION} and Minecraft version ${MINECRAFT_VERSION}.\\nShould you be using unlimited memory value of 0, make sure to increase the default install resource limits in the Wings config or specify exact allocated memory in the server Build Configuration instead of 0! \\nOtherwise, the Forge installer will not have enough memory.\"; exit 4; }\r\n\r\n# Check if we need a symlink for 1.17+ Forge JPMS args\r\nif [[ $MC_VERSION =~ ^1\\.(17|18|19|20|21|22|23) || $FORGE_VERSION =~ ^1\\.(17|18|19|20|21|22|23) ]]; then\r\n  unix_args\r\n\r\n# Check if someone has set MC to latest but overwrote it with older Forge version, otherwise we would have false positives\r\nelif [[ $MC_VERSION == \"latest\" && $FORGE_VERSION =~ ^1\\.(17|18|19|20|21|22|23) ]]; then\r\n  unix_args\r\nelse\r\n  # For versions below 1.17 that ship with jar\r\n  mv $FORGE_JAR $SERVER_JARFILE\r\nfi\r\n\r\necho -e \"Deleting installer.jar file.\\n\"\r\nrm -rf installer.jar\r\necho -e \"Installation process is completed\""
  }
}
```

Sources

- [app/Http/Controllers/Api/Remote/Servers/ServerInstallController.php#L30](https://github.com/pterodactyl/panel/blob/v1.11.3/app/Http/Controllers/Api/Remote/Servers/ServerInstallController.php#L30)

---

### `POST /api/remote/servers/:uuid/install`

Updates the installation state of a server.

### Body

| Name       | Visibility | Type    | Description                                                    |
| ---------- | ---------- | ------- | -------------------------------------------------------------- |
| successful | required   | boolean | Notifies if the server has completed the installation process. |
| reinstall  | required   | boolean | The state of the server.                                       |

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 204  | The request was successful. |
| 404  | The server was not found.   |

Sources

- [app/Http/Controllers/Api/Remote/Servers/ServerInstallController.php#L48](https://github.com/pterodactyl/panel/blob/v1.11.3/app/Http/Controllers/Api/Remote/Servers/ServerInstallController.php#L48)
