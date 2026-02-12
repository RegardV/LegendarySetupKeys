# Claude Code Multi-Provider Setup

Use Claude Code with cheaper AI providers (Z.AI & Kimi K2) instead of Anthropic's API. Save 85-95% on costs while keeping the same powerful coding assistant experience.

## What This Does

- 🚀 **No Login Required** - Skip Anthropic authentication
- 💰 **Massive Savings** - Use Z.AI (GLM-4.7) or Kimi K2 at 85-95% lower cost
- 🔄 **Easy Switching** - Change AI providers with one command
- 🔒 **Secure** - Project-specific configuration, API keys safely stored
- ⚡ **Zero Config Conflicts** - Clean setup, no environment pollution

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

Choose one or both:
- **Z.AI** (GLM-4.7): https://api.z.ai or https://open.bigmodel.cn
- **Kimi K2**: https://platform.moonshot.ai/console

### 3. Run Setup
```bash
# In your project directory
cd ~/your-project

# Run the setup wizard
bash LegendarySetupKeys

# Follow prompts to enter your API keys
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
# Switch to Z.AI (cheap, fast)
./switch-model zai
claude

# Switch to Kimi K2 (powerful reasoning)
./switch-model kimi
claude

# Check current configuration
./check-config
```

## What Gets Installed
```
your-project/
├── .claude/
│   ├── .envc                    # Your API keys (secure)
│   ├── settings.json            # Active config
│   ├── settings.zai.json        # Z.AI template
│   └── settings.kimi.json       # Kimi template
├── switch-model                 # Switch providers
├── check-config                 # View config
└── LegendarySetupKeys          # Setup wizard
```

## Provider Comparison

| Provider | Model | Cost vs Claude | Best For |
|----------|-------|----------------|----------|
| **Z.AI** | GLM-4.7 | ~85% cheaper | General coding, documentation |
| **Kimi K2** | kimi-k2-thinking-turbo | ~90% cheaper | Complex reasoning, debugging |

## Common Commands
```bash
# Switch providers
./switch-model zai                # Use Z.AI
./switch-model kimi               # Use Kimi K2
./switch-model                    # Show current

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

## Configuration Files

- **`.claude/.envc`** - Your API keys (keep secure, add to .gitignore)
- **`.claude/settings.json`** - Active configuration (changes when you switch)
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
alias cc='cd ~/your-project && ./check-config'

# Use anywhere
cz    # Start with Z.AI
ck    # Start with Kimi
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

## FAQ

**Q: Do I need an Anthropic API key?**  
A: No! This uses Z.AI and Kimi keys instead.

**Q: Can I use multiple providers at once?**  
A: No, switch between them with `./switch-model [zai|kimi]`

**Q: Which provider should I use?**  
A: Start with Z.AI for general work, switch to Kimi for complex problems.

**Q: Is my data sent to Anthropic?**  
A: No, requests go directly to Z.AI or Kimi K2.

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
./switch-model zai     # Use Z.AI
./switch-model kimi    # Use Kimi K2
claude                 # Start coding

# Inside Claude
/status                # Check config
/help                  # Get help
Ctrl+C (twice)         # Exit
```

**Need help?** Run `./check-config` or see `CLAUDE-CODE-MANUAL.md`

---

*Legendary Team 2026 | Last Updated: 2026-02-12*
