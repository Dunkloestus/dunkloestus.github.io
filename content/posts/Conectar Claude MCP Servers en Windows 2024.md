---
created: 2024-11-14T02:00
updated: 2024-11-29T07:21
title: Conectar Claude MCP Servers en Windows 2024
date: 2024-11-29T11:07:07+01:00
draft: "false"
share: "true"
type: post
tags:
  - Claude
  - MCP
  - Windows
  - npm
  - npx
  - IA
  - tutoriales
  - Español
  - Guias
showTableOfContents: "true"
---

![](/images/Pasted%20image%2020241129053405.png)
# Claude tiene algunos errores en Win11

a la fecha 29-11-24 Claude Desktop presenta errores al conectarse con ell MCP Server debido a un paquete de npx con incompatibilidad en windows si visitas el GitHub Repo te dan un ejemplo así:


```
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "/Users/username/Desktop",
        "/path/to/other/allowed/dir"
      ]
    }
  }
}
```

Y si lo intentas claude desktop soltara un mensaje como "Claude no se puede conectar a el servidor MCP *insert service name*"

la solución es usar directamente npm y instalar las variables de forma global con -g
y luego configurar los servidores directamente, aqui dejo un ejemplo de varios servicios incluyendo github, filesystem y mas.

recuerda tambien tener instalado node.js y agregarlo al PATH de tu maquina

```
{

    "mcpServers": {

        "github": {

        "command": "node",

        "args": ["C:\\Users\\your_name_here\\AppData\\Roaming\\npm\\node_modules\\@modelcontextprotocol\\server-github\\dist\\index.js"],  

        "env": {

          "GITHUB_PERSONAL_ACCESS_TOKEN": "AQUI VA TU TOKEN DE GITHUB"

        }

      },

    "filesystem": {

        "command": "node",

        "args": [

            "C:\\Users\\your_name_here\\AppData\\Roaming\\npm\\node_modules\\@modelcontextprotocol\\server-filesystem\\dist\\index.js",

            "C:\\" , "AQUI EL SITIO DONDE QUIERES QUE TENGA ACCESO CLAUDE"

            ]

          },

      "everything": {

      "command": "node",

      "args": ["C:\\Users\\your_name_here\\AppData\\Roaming\\npm\\node_modules\\@modelcontextprotocol\\server-everything\\dist\\index.js"],

      "env": {

        "DEBUG": "*"

      }

    },

        "memory": {

      "command": "node",

      "args": ["C:\\Users\\your_name_here\\AppData\\Roaming\\npm\\node_modules\\@modelcontextprotocol\\server-memory\\dist\\index.js"],

      "env": {

        "DEBUG": "*"

      }

    }

    }

  }
```


Creo que eso es todo, quería compartir algo y revivir el sitio. 