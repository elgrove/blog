---
layout: post
title: "VS Code as a note-taking app"
description: 
summary: 
---

## VS Code Server docker container from linuxserver.io

```yaml
  code-server:
    image: lscr.io/linuxserver/code-server
    container_name: code-server
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
      - PASSWORD=pass
      - SUDO_PASSWORD=passs
      - PROXY_DOMAIN=my_domain
      - DEFAULT_WORKSPACE=/notes
    volumes:
      - ./codeserver:/config
      - ./notes:/notes
    ports:
      - 8443:8443
    restart: unless-stopped
```

## emeraldwalk's Run on Save extension

Command pallette command Run on Save: enable/disable is handy

```json
    "emeraldwalk.runonsave": {
        "commands": [
            {
                "match": "\\.md$",
                "cmd": "cd /notes; git add .; git commit -m '.'; git push origin main"
            },
        ]
    }
```

