# Claude Code Multi-Provider Setup

Use Claude Code with cheaper (or free local) AI providers instead of Anthropic's API. Save 85-95% on costs or run completely free with local models.

## What This Does

- **No Login Required** - Skip Anthropic authentication
- **4 Providers** - Z.AI, Kimi K2, OpenRouter (400+ models), LM Studio (local)
- **Easy Switching** - Change AI providers with one command
- **Secure** - Project-specific configuration, API keys safely stored
- **Zero Config Conflicts** - Clean setup, no environment pollution

## Prerequisites
```bash
# Required
node -v    # v18.0+
npm -v     # v10.0+

# Install if needed
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs
```

## Quick Start (5 Minutes)

### 1. Install Claude Code
```bash
npm install -g @anthropic-ai/claude-code
claude --version
```

### 2. Get API Keys

Choose any combination:
- **Z.AI** (GLM-4.7): https://api.z.ai or https://open.bigmodel.cn (~$3-15/mo)
- **Kimi K2**: https://platform.moonshot.ai/console
- **OpenRouter** (400+ models): https://openrouter.ai/keys (pay-per-use, access to Grok, GPT, Gemini, DeepSeek, etc.)
- **LM Studio** (free, local): https://lmstudio.ai/download (v0.4.1+ required)

### 3. Run Setup
```bash
# In your project directory
cd ~/your-project

# Run the setup wizard
bash LegendarySetupKeys

# Follow prompts to configure providers
```

### 4. Start Using
```bash
# Start Claude Code
claude

# Check configuration
/status
```

## Daily Usage
```bash
# Switch providers
./switch-model zai          # Z.AI (cheap, fast)
./switch-model kimi         # Kimi K2 (reasoning)
./switch-model openrouter   # OpenRouter (400+ models)
./switch-model lmstudio     # LM Studio (free, local)

# Check current configuration
./check-config

# Start Claude Code
claude
```

## What Gets Installed
```
your-project/
├── .claude/
│   ├── .envc                       # Your API keys (secure)
│   ├── settings.json               # Active config
│   ├── settings.zai.json           # Z.AI template
│   ├── settings.kimi.json          # Kimi template
│   ├── settings.openrouter.json    # OpenRouter template
│   └── settings.lmstudio.json     # LM Studio template
├── switch-model                    # Switch providers
├── check-config                    # View config
└── LegendarySetupKeys             # Setup wizard
```

## Provider Comparison

| Provider | Model(s) | Cost | Best For |
|----------|----------|------|----------|
| **Z.AI** | GLM-4.7 | ~$3-15/mo | General coding, documentation |
| **Kimi K2** | kimi-k2-thinking-turbo | ~90% cheaper | Complex reasoning, debugging |
| **OpenRouter** | 400+ (Grok, GPT, Gemini, etc.) | Pay-per-use | Flexibility, access to any model |
| **LM Studio** | Any local GGUF/MLX model | Free | Privacy, offline, no API costs |

## API Endpoints

All providers expose **Anthropic-compatible** endpoints that Claude Code connects to:

| Provider | Base URL | Notes |
|----------|----------|-------|
| **Z.AI** | `https://api.z.ai/api/anthropic` | Anthropic-compatible ([docs](https://docs.z.ai/scenario-example/develop-tools/claude)) |
| **Kimi K2** | `https://api.moonshot.ai/anthropic` | Anthropic-compatible |
| **OpenRouter** | `https://openrouter.ai/api` | Anthropic-compatible ([docs](https://openrouter.ai/docs/guides/guides/claude-code-integration)) |
| **LM Studio** | `http://localhost:1234` | Local Anthropic-compatible ([docs](https://lmstudio.ai/docs/integrations/claude-code)) |

> **Note on Z.AI:** Z.AI has multiple endpoints (`/api/paas/v4`, `/api/coding/paas/v4`), but Claude Code requires the **Anthropic-compatible** endpoint (`/api/anthropic`).

> **Note on x.ai Grok:** x.ai deprecated their Anthropic-compatible endpoint. Use **OpenRouter** to access Grok models (e.g. `x-ai/grok-4`).

## OpenRouter — Access Any Model

OpenRouter gives you access to 400+ models through a single API key. After setup, edit `.claude/settings.openrouter.json` to use any model:

```bash
# Popular models you can use via OpenRouter:
x-ai/grok-4                        # xAI Grok 4
google/gemini-2.5-pro               # Google Gemini
deepseek/deepseek-r1                # DeepSeek R1
meta-llama/llama-4-maverick         # Meta Llama 4
anthropic/claude-sonnet-4-5         # Claude (default)
```

## LM Studio — Free Local Models

Run models completely locally with no API costs and full privacy:

1. Install [LM Studio](https://lmstudio.ai/download) (v0.4.1+)
2. Download a model (recommended: qwen2.5-coder-32b, deepseek-coder-v2, codellama)
3. Start the LM Studio server (it runs on port 1234 by default)
4. Run the setup wizard and choose LM Studio
5. `./switch-model lmstudio && claude`

Requirements: LM Studio v0.4.1+ with the Anthropic-compatible server enabled. At least 25K context window recommended.

## Common Commands
```bash
# Switch providers
./switch-model zai                # Use Z.AI
./switch-model kimi               # Use Kimi K2
./switch-model openrouter         # Use OpenRouter
./switch-model lmstudio           # Use LM Studio
./switch-model                    # Show current + available

# Check status
./check-config                    # View configuration
claude                            # Start Claude Code
/status                           # Check inside Claude

# Update keys
bash LegendarySetupKeys           # Re-run setup wizard
nano .claude/.envc                # Edit keys directly
```

## Troubleshooting

### "Auth conflict" error
```bash
# Clear environment variables
unset ANTHROPIC_API_KEY
unset ANTHROPIC_AUTH_TOKEN

# Clear global settings
echo '{}' > ~/.claude/settings.json

# Restart
claude
```

### "Command not found: claude"
```bash
# Add npm to PATH
echo 'export PATH="$HOME/.npm-global/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

### "API timeout" or connection errors
```bash
# Re-test and update keys
bash LegendarySetupKeys
```

### LM Studio not connecting
```bash
# Check LM Studio server is running
curl http://localhost:1234/v1/models

# If different port, re-run setup
bash LegendarySetupKeys
```

### OpenRouter returning errors
```bash
# Ensure ANTHROPIC_API_KEY is empty (not unset)
# The setup wizard handles this automatically
# If issues persist, re-run setup
bash LegendarySetupKeys
```

## Configuration Files

- **`.claude/.envc`** - Your API keys (keep secure, add to .gitignore)
- **`.claude/settings.json`** - Active configuration (changes when you switch)
- **`.claude/settings.*.json`** - Provider templates (static, re-created by setup)
- **`~/.claude.json`** - Global skip-login setting

## Security Notes
```bash
# Always verify permissions
ls -la .claude/.envc
# Should show: -rw------- (600)

# Add to .gitignore
echo ".claude/.envc" >> .gitignore

# Never commit API keys!
```

## Advanced Usage

### Add Shell Aliases
```bash
# Add to ~/.bashrc
alias cz='cd ~/your-project && ./switch-model zai && claude'
alias ck='cd ~/your-project && ./switch-model kimi && claude'
alias co='cd ~/your-project && ./switch-model openrouter && claude'
alias cl='cd ~/your-project && ./switch-model lmstudio && claude'
alias cc='cd ~/your-project && ./check-config'

# Use anywhere
cz    # Start with Z.AI
ck    # Start with Kimi
co    # Start with OpenRouter
cl    # Start with LM Studio (local)
```

### Multiple Projects
```bash
# Copy setup to other projects
cp LegendarySetupKeys ~/other-project/
cd ~/other-project
bash LegendarySetupKeys

# Each project has independent configuration
```

## Documentation

- **Full Manual**: See `CLAUDE-CODE-MANUAL.md` for comprehensive documentation
- **Claude Code Docs**: https://docs.claude.com/claude-code
- **Z.AI**: https://api.z.ai
- **Kimi**: https://platform.moonshot.ai
- **OpenRouter**: https://openrouter.ai
- **LM Studio**: https://lmstudio.ai

## FAQ

**Q: Do I need an Anthropic API key?**
A: No! This uses alternative providers instead.

**Q: Can I use multiple providers at once?**
A: No, but you can switch instantly with `./switch-model [provider]`

**Q: Which provider should I use?**
A: Z.AI for budget coding, OpenRouter for model flexibility, LM Studio for privacy/free usage, Kimi for complex reasoning.

**Q: Can I use x.ai Grok?**
A: Yes, via OpenRouter. Set the model to `x-ai/grok-4` in `.claude/settings.openrouter.json`.

**Q: What local models work best with LM Studio?**
A: qwen2.5-coder-32b, deepseek-coder-v2, and codellama work well. Models need tool-use support for best results.

**Q: Is my data sent to Anthropic?**
A: No, requests go directly to whichever provider you configure.

**Q: How do I uninstall?**
A: `rm -rf .claude/ switch-model check-config LegendarySetupKeys`

## Support

Having issues? Check:
1. `./check-config` - View your configuration
2. `claude --version` - Verify installation
3. `bash LegendarySetupKeys` - Re-test keys
4. See `CLAUDE-CODE-MANUAL.md` for detailed troubleshooting

## License

MIT - Use freely, no warranty provided.

---

**Quick Reference Card**
```bash
# Setup (once)
bash LegendarySetupKeys

# Daily use
./switch-model zai          # Z.AI (~$3/mo)
./switch-model kimi         # Kimi K2
./switch-model openrouter   # 400+ models (Grok, GPT, Gemini...)
./switch-model lmstudio     # Free local models
claude                      # Start coding

# Inside Claude
/status                # Check config
/help                  # Get help
Ctrl+C (twice)         # Exit
```

**Need help?** Run `./check-config` or see `CLAUDE-CODE-MANUAL.md`

---

*Legendary Team 2026 | Last Updated: 2026-02-13*
