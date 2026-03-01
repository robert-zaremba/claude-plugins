# Claude Code Plugins

A collection of plugins for [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

## Available Plugins

| Plugin                      | Description                         |
|-----------------------------|-------------------------------------|
| [vuejs-nuxt-bun](./vuejs-nuxt/) | LSP for Vue.js with skills for Nuxt |

## Setup

### Requirements

+ Bun (instead of Node+npm)
+ typescript-language-server  >= 5.1
+ typescript-language-server  >= 3.2

### Add the Marketplace

Run the following slash command in Claude Code:

```
/plugin marketplace add robert-zaremba/claude-plugins
```

### Browse and Install Plugins

List available plugins:

```
/plugin marketplace list
```

Install a plugin:

```
/plugin install <plugin-name>@local-plugins
```

### Alternative: Settings File

Add the marketplace to your Claude Code settings file (`~/.claude/settings.json`
or `.claude/settings.json` in your project):

```json
{
  "extraKnownMarketplaces": {
    "local-plugins": {
      "source": {
        "source": "github",
        "repo": "robert-zaremba/claude-plugins"
      }
    }
  }
}
```
