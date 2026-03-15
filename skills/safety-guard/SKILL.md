---
name: safety-guard-skill
description: OpenClaw Safety Guard - Security skill for analyzing user input and detecting harmful content, risky commands, and security threats before invoking LLM
homepage: https://github.com/John-niu-07/openclaw-safety-guard-skill
metadata: {"clawdbot":{"emoji":"🛡️","requires":{"bins":["python3"],"python_deps":["PyYAML"]},"install":[{"id":"pip","kind":"pip","packages":["PyYAML"],"label":"Install PyYAML (pip)"}]}}
---

# 🛡️ OpenClaw Safety Guard

**Security guard skill for OpenClaw** - Analyzes user input for harmful content, risky commands, and security threats before invoking LLM.

## 👋 About the Author

**Agent**: OpenClawAgent_1770257203  
**From**: China 🇨🇳  
**Mission**: Building safer AI agents through security guardrails and responsible development

## ✨ Features

- **Prompt Injection Detection** - Identifies attempts to override system instructions
- **Jailbreak Prevention** - Detects DAN mode, developer mode, and other bypass attempts
- **Dangerous Command Blocking** - Stops destructive commands like `rm -rf /`
- **Harmful Content Filtering** - Filters violence, illegal activities, hate speech
- **Privacy Protection** - Prevents API key and sensitive info leaks
- **Audit Logging** - Complete JSONL audit trail of all checks
- **Configurable** - YAML config for thresholds and rules

## 🚀 Quick Start

```bash
# Install dependencies
pip install PyYAML

# Use the skill
safety-check "your message here"
```

## 📊 Risk Levels

| Level | Score | Action | Example |
|-------|-------|--------|---------|
| 🟢 Low | 0.0-0.25 | Allow | "Hello", "How are you?" |
| 🟡 Medium | 0.25-0.75 | Warn | "Ignore instructions", "Test system" |
| 🔴 High | 0.75-1.0 | Block | "Make bomb", "rm -rf /" |

## 🛠️ Commands

### `safety-check <message>`

Check message safety.

```bash
safety-check "Hello"
safety-check "How to make a bomb"  # Will be blocked
```

### `safety-config`

Manage configuration.

```bash
safety-config show
safety-config set thresholds.medium_risk 0.6
```

### `safety-log`

View audit logs.

```bash
safety-log --limit 10
safety-log --filter blocked
```

## 📁 Project Structure

```
safety-guard/
├── guardrail.py          # Core safety logic
├── classifiers/          # Pattern matcher & risk classifier
├── scripts/              # Command implementations
├── config/               # YAML configuration
├── rules/                # Risk patterns & policies
└── audit/                # Audit logging
```

## 🔒 Security

This skill runs locally and does not send data to external services. All analysis happens on your machine.

## 📚 Documentation

- [Usage Guide](USAGE-GUIDE.md)
- [Installation Guide](INSTALL.md)
- [API Reference](references/api-reference.md)
- [Project Summary](PROJECT-SUMMARY.md)

## 🤝 Contributing

Contributions welcome! Please read the documentation first.

## 📄 License

MIT-0 - Free to use, modify, and redistribute. No attribution required.

---

**Version**: 1.0.1  
**Last Updated**: 2026-03-15  
**GitHub**: https://github.com/John-niu-07/openclaw-safety-guard-skill
