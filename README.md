# Claude Code Bridge (ccb)

A tool for switching between different Claude Code service providers.

## Features

- Switch between multiple Claude Code providers with a simple command
- Interactive provider selection menu
- Support for custom API endpoints and authentication
- Environment variable management for different providers
- Default provider support for quick access to your preferred provider

## Installation

### Homebrew (recommended)

```bash
brew tap iuhoay/claude-code-bridge
brew install claude-code-bridge
```

### Manual

1. Make the `ccb` script executable:
   ```bash
   chmod +x ccb
   ```

2. Move it to your PATH (optional):
   ```bash
   mv ccb /usr/local/bin/
   ```

## Configuration

Create a configuration file at `~/.config/claude_code_bridge/providers.json`:

```json
{
  "default_provider": "anthropic",
  "providers": {
    "anthropic": {
      "name": "Anthropic Official",
      "description": "Uses Claude Code's default configuration, no environment variables needed"
    },
    "z_ai": {
      "name": "Z.AI",
      "env": {
        "ANTHROPIC_AUTH_TOKEN": "your_api_key_here",
        "ANTHROPIC_BASE_URL": "https://api.z.ai/api/anthropic",
        "ANTHROPIC_DEFAULT_HAIKU_MODEL": "glm-4.5-air",
        "ANTHROPIC_DEFAULT_SONNET_MODEL": "glm-4.7",
        "ANTHROPIC_DEFAULT_OPUS_MODEL": "glm-4.7"
      }
    },
    "kimi": {
      "name": "Kimi",
      "env": {
        "ANTHROPIC_AUTH_TOKEN": "your_kimi_api_key_here",
        "ANTHROPIC_BASE_URL": "https://api.moonshot.cn/anthropic",
        "ANTHROPIC_DEFAULT_HAIKU_MODEL": "kimi-k2.5",
        "ANTHROPIC_DEFAULT_SONNET_MODEL": "kimi-k2.5",
        "ANTHROPIC_DEFAULT_OPUS_MODEL": "kimi-k2.5"
      }
    }
  }
}
```

**Configuration Options:**
- `default_provider`: (Optional) The provider key to use by default when no provider is specified
- `providers`: Object containing provider configurations keyed by provider name

## Usage

### Default provider or interactive selection
```bash
ccb                    # Uses default provider if set, otherwise shows interactive menu
```

### Direct provider selection
```bash
ccb anthropic          # Use specific provider
ccb z_ai --help        # Use Z.AI provider and pass --help to Claude
```

### Setting a default provider
```bash
ccb --set-default z_ai # Set Z.AI as the default provider
```

### Show help
```bash
ccb --help
```

## Requirements

- `jq` for JSON parsing
- Claude Code installed

## Environment Variables

- `CCB_CONFIG_DIR`: Configuration directory (default: `~/.config/claude_code_bridge`)
- `CCB_CONFIG_FILE`: Configuration file path (default: `$CCB_CONFIG_DIR/providers.json`)
