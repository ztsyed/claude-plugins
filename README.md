# Claude Code Plugins - ztsyed

Shared Claude Code plugins for distributed systems development.

## Quick Start

### Add the Marketplace

```bash
claude /plugin marketplace add ztsyed/claude-plugins
```

### Install Plugins

```bash
claude /plugin install ztsyed-plugins
```

### Verify Installation

```bash
claude /plugin list
```

## Available Components

### Agents

| Agent | Usage | Description |
|-------|-------|-------------|
| distributed-systems | `@distributed-systems` | NATS, event-driven architecture, alarm management |
| architecture-reviewer | `@architecture-reviewer` | System design review for scalability/reliability |
| multi-repo-coordinator | `@multi-repo-coordinator` | Cross-repository change coordination |

### Commands

| Command | Description |
|---------|-------------|
| `/ztsyed-plugins:review` | Comprehensive code review |
| `/ztsyed-plugins:pipeline-check` | Validate NATS/n8n pipelines |

### Skills (Auto-Invoked)

| Skill | Triggers On |
|-------|-------------|
| nats-patterns | NATS, JetStream, messaging code |
| n8n-workflows | n8n, workflow, webhook code |

## Usage Examples

```bash
# Ask the distributed systems expert
claude @distributed-systems "Review my NATS consumer implementation"

# Get architecture feedback
claude @architecture-reviewer "Analyze this microservice design"

# Coordinate multi-repo changes
claude @multi-repo-coordinator "I need to update the schema in repo A and consumers in repo B"

# Run a code review
claude /ztsyed-plugins:review

# Check pipeline configs
claude /ztsyed-plugins:pipeline-check
```

## Updating

```bash
claude /plugin update ztsyed-plugins
```

## Contributing

1. Fork this repository
2. Create a feature branch
3. Add/modify agents, commands, or skills
4. Submit a pull request

## License

MIT
