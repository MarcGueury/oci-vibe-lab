# Vibe Coding - Database

## Introduction
In this lab, you will install the SQLcl MCP tool to help the agent to generate code about the database.

Estimated time: 10 min

### Objectives

- Test the program using a LangGraph user interface.

### Prerequisites
- The lab 1 must have been completed.

## Task 1: Add the SQLcl MCP Server to Cline.

1. With the Cline extension selected on the sidebar, click Manage MCP Servers Manage MCP Servers icon below the prompt box.
2. In the resulting dialogue, click Settings Settings icon.
3. The MCP Servers page opens, with the Installed tab selected.
4. Click Configure MCP Servers.
5.  The cline\_mcp\_settings.json file opens in the VS Code editor.
6. In the settings file, add a JSON configuration snippet in the following format. Replace PATH/bin/sql with the absolute path of your SQLcl installation, and press Ctrl+S on your keyboard to save the file.
    ```
    {
        "mcpServers": {
            "SQLcl": {
                "command": "PATH/bin/sql",
                "args": ["-mcp"],
                "disabled": false
            }
        }
    }
    ```
7. You’ll now see the SQLcl MCP Server and its tools listed on the MCP Servers page.
    Click Done on the MCP Servers page.
8. If necessary, restart VS Code for changes to take effect.

See also: https://www.thatjeffsmith.com/archive/2025/07/getting-started-with-our-mcp-server-for-oracle-database/

## Task 2: Setup the connection

XXX

## Task 3: Generating documentation about existing tables

XXX

## Task 4: Generating SQL and PL/SQL code 

XXX

## Task 5: Generating MCP tools

XXX


## Known issues

None

## Acknowledgements

- **Author**
    - Marc Gueury, Generative AI Specialist
    - Ilayda Temir, Generative AI Specialist

