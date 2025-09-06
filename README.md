# Claude Code Bridge (ccb)

A tool for switching between different Claude Code service providers.

## Features

- Switch between multiple Claude Code providers with a simple command
- Interactive provider selection menu
- Support for custom API endpoints and authentication
- Environment variable management for different providers

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
  "providers": {
    "anthropic": {
      "name": "Anthropic Official",
      "description": "Uses Claude Code's default configuration, no environment variables needed"
    },
    "z_ai": {
      "name": "Z.AI",
      "base_url": "https://api.z.ai/api/anthropic",
      "auth_token": "your_z_ai_token_here",
      "model": "GLM-4.5",
      "small_model": "GLM-4.5-X"
    }
  }
}
```

## Usage

### Interactive selection
```bash
ccb
```

### Direct provider selection
```bash
ccb anthropic
ccb z_ai --help
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