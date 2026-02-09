# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Claude Code Bridge (ccb) is a shell script tool that enables switching between different Claude Code service providers. It allows users to interactively select from multiple API providers (Anthropic, Z.AI, Kimi, etc.) and sets the appropriate environment variables before launching Claude Code.

## Architecture

### Core Components

- **`ccb`**: Main bash script that handles provider selection and Claude Code execution
- **`tap/claude-code-bridge.rb`**: Homebrew formula for installation
- **`.claude_providers.json.example`**: Example provider configuration file

### Provider Configuration System

The tool uses a JSON configuration file stored at `~/.config/claude_code_bridge/providers.json` that defines available providers with their:
- `name`: Display name for the provider
- `description`: Optional description
- `env`: Object containing environment variables to set (key-value pairs)

Environment variables are set directly from the `env` object for each provider, allowing full control over which variables are set.

Example provider configuration:
```json
{
  "z_ai": {
    "name": "Z.AI",
    "env": {
      "ANTHROPIC_AUTH_TOKEN": "your_token",
      "ANTHROPIC_BASE_URL": "https://api.z.ai/api/anthropic",
      "ANTHROPIC_DEFAULT_HAIKU_MODEL": "glm-4.5-air"
    }
  }
}
```

## Development Commands

### Testing the Tool
```bash
# Test help functionality
./ccb --help

# Test interactive provider selection
./ccb

# Test direct provider execution
./ccb anthropic --help
```

### Homebrew Formula Development
```bash
# Test formula installation
brew install --debug --verbose ./tap/claude-code-bridge.rb

# Test formula uninstallation
brew uninstall claude-code-bridge

# Update formula (edit tap/claude-code-bridge.rb)
# Then update tap submodule:
cd tap && git pull origin main && cd ..
git add tap && git commit -m "chore: update tap submodule"
```

### Configuration Management
```bash
# View current config
cat ~/.config/claude_code_bridge/providers.json

# Test config parsing
jq '.providers' ~/.config/claude_code_bridge/providers.json
```

## Dependencies

- **jq**: Required for JSON parsing in the bash script
- **Claude Code**: Must be installed and available in PATH
- **Bash 4+**: Script uses modern bash features

## File Structure Notes

- The main script (`ccb`) must remain executable
- Provider configurations use an `env` object with explicit environment variable names
- The `anthropic` provider is special-cased - no environment variables are set for it
- Homebrew tap is included as a git submodule at `tap/`

## Testing Considerations

- Validate JSON syntax of provider configurations
- Test environment variable setting for each provider type
- Verify Claude Code launches with correct provider context
- Test error handling for missing configs, invalid JSON, missing jq
- Ensure executable permissions are maintained on the `ccb` script