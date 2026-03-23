# Installation Guide

This guide shows you how to install CockroachDB Skills for use with Claude Code.

## Prerequisites

- **Claude Code** - [Download and install Claude Code](https://claude.ai/download)
- **Git** - For cloning the repository

## Installation Options

Choose the approach that fits your workflow:

### Option 1: Project-Level Installation (Recommended for Teams)

Skills are available only within a specific project directory.

**When to use:** Working on a CockroachDB project and want these skills available only in that context.

```bash
# 1. Clone the repository
git clone https://github.com/cockroachlabs/cockroachdb-skills.git

# 2. Navigate to your project directory
cd /path/to/your-cockroachdb-project

# 3. Create the skills directory
mkdir -p .claude/skills

# 4. Create a symlink to the skills
ln -s /path/to/cockroachdb-skills/skills .claude/skills/cockroachdb-skills
```

### Option 2: User-Level Installation (Global Access)

Skills are available in all Claude Code sessions, across all projects.

**When to use:** You work with CockroachDB frequently and want these skills always available.

```bash
# 1. Clone the repository
git clone https://github.com/cockroachlabs/cockroachdb-skills.git

# 2. Create the user-level skills directory
mkdir -p ~/.claude/skills

# 3. Create a symlink to the skills
ln -s /path/to/cockroachdb-skills/skills ~/.claude/skills/cockroachdb-skills
```

### Option 3: Direct Copy (Without Symlinks)

For environments where symbolic links aren't supported (some Windows configurations).

**Project-level:**
```bash
# Clone and copy to project
git clone https://github.com/cockroachlabs/cockroachdb-skills.git
mkdir -p /path/to/your-project/.claude/skills
cp -r cockroachdb-skills/skills /path/to/your-project/.claude/skills/cockroachdb-skills
```

**User-level:**
```bash
# Clone and copy to user directory
git clone https://github.com/cockroachlabs/cockroachdb-skills.git
mkdir -p ~/.claude/skills
cp -r cockroachdb-skills/skills ~/.claude/skills/cockroachdb-skills
```

**Note:** When using the copy method, you'll need to manually update the skills when the repository is updated.

## Verification

After installation, verify that Claude Code can discover the skills:

### 1. Start Claude Code

Start Claude Code in a terminal or open it in your IDE.

### 2. Ask Claude to List Skills

```
What CockroachDB skills are available?
```

**Expected response:**
Claude should list the skills grouped by domain, such as:
- Onboarding and Migrations (molt-fetch, molt-verify, molt-replicator)
- Performance and Scaling (analyzing-range-distribution, profiling-statement-fingerprints)
- Security and Governance (configuring-sso-and-scim, managing-tls-certificates)
- Operations and Lifecycle (reviewing-cluster-health, upgrading-cluster-version)
- And more...

### 3. Test a Skill

Try invoking a skill by describing a task:

```
Help me check if my CockroachDB cluster is healthy
```

Claude should use the `reviewing-cluster-health` skill to provide guidance.

## Troubleshooting

### Skills Not Discovered

**Problem:** Claude doesn't recognize the CockroachDB skills.

**Solutions:**
1. **Check directory structure:**
   ```bash
   # For project-level
   ls -la .claude/skills/cockroachdb-skills/

   # For user-level
   ls -la ~/.claude/skills/cockroachdb-skills/
   ```

   You should see skill directories like `onboarding-and-migrations/`, `security-and-governance/`, etc.

2. **Verify SKILL.md files exist:**
   ```bash
   find .claude/skills/cockroachdb-skills -name "SKILL.md"
   ```

   This should return multiple SKILL.md files.

3. **Restart Claude Code** - Sometimes a restart is needed for skill discovery.

4. **Check symlink:**
   ```bash
   # Verify symlink points to correct location
   ls -l .claude/skills/cockroachdb-skills
   ```

### Permission Errors

**Problem:** Permission denied when creating symlinks or directories.

**Solutions:**
- On macOS/Linux: Use `sudo` if needed for user-level installation
- On Windows: Run terminal as Administrator
- Check file permissions: `chmod` and `chown` as needed

### Symlink Not Supported

**Problem:** Your environment doesn't support symbolic links.

**Solution:** Use [Option 3: Direct Copy](#option-3-direct-copy-without-symlinks) instead.

### Skills Appear Outdated

**Problem:** Skills don't reflect recent repository updates.

**Solutions:**

**If using symlinks:**
```bash
# Navigate to the cloned repository
cd /path/to/cockroachdb-skills

# Pull latest changes
git pull origin main
```

**If using direct copy:**
```bash
# Pull latest changes
cd /path/to/cockroachdb-skills
git pull origin main

# Re-copy to installation location
# For project-level:
cp -r skills /path/to/your-project/.claude/skills/cockroachdb-skills

# For user-level:
cp -r skills ~/.claude/skills/cockroachdb-skills
```

## Updating Skills

### With Symlinks (Options 1 & 2)

Simply pull the latest changes from the repository:

```bash
cd /path/to/cockroachdb-skills
git pull origin main
```

The symlink ensures Claude Code automatically uses the updated skills.

### With Direct Copy (Option 3)

After pulling updates, re-copy the skills:

```bash
cd /path/to/cockroachdb-skills
git pull origin main

# Then copy to your installation location (see Option 3 above)
```

## Uninstalling

### Remove Project-Level Skills

```bash
rm .claude/skills/cockroachdb-skills
```

### Remove User-Level Skills

```bash
rm ~/.claude/skills/cockroachdb-skills
```

Or if you used direct copy:

```bash
rm -rf ~/.claude/skills/cockroachdb-skills
```

## Next Steps

- **[Usage Guide](usage.md)** - Learn how to discover and invoke skills
- **[Browse Skills](../skills/)** - Explore available skills by domain
- **[Contributing](../CONTRIBUTING.md)** - Help improve these skills

## Getting Help

- **[CockroachDB Documentation](https://www.cockroachlabs.com/docs/)** - Official CockroachDB docs
- **[Claude Code Documentation](https://claude.ai/docs)** - Claude Code features and usage
- **[GitHub Issues](https://github.com/cockroachlabs/cockroachdb-skills/issues)** - Report problems or request features
