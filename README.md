# AI Agent Skills & Plugins

A collection of plugins for

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code).
- [OpenCode](https://opencode.ai/)
- [Kilo](https://github.com/Kilo-Org/kilocode/)

## Available Plugins

| Plugin                              | Description                         |
| ----------------------------------- | ----------------------------------- |
| [vuejs-nuxt-bun](./vuejs-nuxt-bun/) | LSP for Vue.js with skills for Nuxt |

## Requirements

- Bun (instead of Node+npm)
- typescript-language-server >= 5.1
- vue-language-server >= 3.2

### OpenCode / Kilo Code Setup

1. Clone this repository
2. Link `vuejs-nuxt-bun/skills/*` into `~/.config/opencode/skills`. For Kilo Code: `~/.config/kilo/skills/`.

   ```sh
   cd ~/.config/opencode/skills
   ln -s <ai-agent-skills-repo>/vuejs-nuxt-bun/skills/* ./
   ```

Pro tip: if you use both Kilo and OpenCode, then link OpenCode skills into your KiloCode

### Claude Code Setup

#### Option 1: Marketplace

Run the following slash command in Claude Code:

```
/plugin marketplace add robert-zaremba/ai-agent-skills
```

List available plugins:

```
/plugin marketplace list
```

Install a plugin:

```
/plugin install <plugin-name>@local-plugins
```

#### Option 2: Clone to Claude config directory

```bash
# Clone to your Claude Code config directory
git clone https://github.com/robert-zaremba/ai-agent-skills.git

ln -s <repo dir>/vuejs-nuxt-bun ~/.claude/plugins/

# Skills are automatically discovered from:
# ~/.claude/plugins/vuejs-nuxt-bun/skills/*/SKILL.md
```

#### Option 3: Settings File

Add the marketplace to your Claude Code settings file (`~/.claude/settings.json`
or `.claude/settings.json` in your project):

```json
{
  "extraKnownMarketplaces": {
    "local-plugins": {
      "source": {
        "source": "github",
        "repo": "robert-zaremba/ai-agent-skills"
      }
    }
  }
}
```

## Setup using project-level installation

Instead of cloning / linking into a global config, you can use your project level directories:

- OpenCode: `<your-project>/.opencode/skills`
- Claud Code: `<your-project>/.claud/plugins`

## LSP

#### Opencode

Opencode uses `opencode.json` for LSP configuration. Add this to your project or global config:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "lsp": {
    "vue-typescript": {
      "command": ["bunx", "--yes", "typescript-language-server", "--stdio"],
      "extensions": [
        ".vue",
        ".ts",
        ".tsx",
        ".mts",
        ".cts",
        ".js",
        ".jsx",
        ".mjs",
        ".cjs"
      ],
      "initialization": {
        "plugins": [
          {
            "name": "@vue/typescript-plugin",
            "location": "@vue/typescript-plugin",
            "languages": ["vue"]
          }
        ]
      }
    }
  }
}
```

**Note:** Opencode has a built-in Vue LSP that auto-installs. The custom configuration above uses `bunx` instead of `npx` for Bun-based projects.

## Using Skills

#### Claude Code

Skills are automatically loaded when the agent detects relevant file types or tasks. You can also explicitly request:

```
Use the vue skill to help me create a new component
```

#### Opencode

Skills are loaded on-demand via the `skill` tool. The agent will automatically discover and load relevant skills:
