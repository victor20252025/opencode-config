# opencode config

my custom opencode setup

## tools

### git-context

get current git state - branch, status, recent commits, diff stats.

### repo-explorer

explore and analyze github repos locally. clones repos to `~/.opencode-repos/` with caching.

| tool | description |
|------|-------------|
| `repo_clone` | clone/update a repo, shows file count and extensions |
| `repo_structure` | directory tree with configurable depth |
| `repo_search` | ripgrep search with regex support |
| `repo_ast` | ast-grep structural search |
| `repo_deps` | analyze package.json, requirements.txt, go.mod, Cargo.toml |
| `repo_hotspots` | find most changed files, largest files, TODOs |
| `repo_find` | find files by pattern using fd |
| `repo_exports` | map public API exports |
| `repo_file` | read file contents with optional line range |
| `repo_cleanup` | remove cached repos |

### swarm tools

multi-agent parallel execution system. splits complex tasks into subtasks, spawns worker agents in parallel, reviews code changes.

| tool | description |
|------|-------------|
| `swarm_init` | start a swarm session, saves git state |
| `swarm_plan_prompt` | get decomposition prompt |
| `swarm_plan_validate` | validate task breakdown |
| `swarm_worktree_create` | create isolated git worktree for a task |
| `swarm_spawn` | spawn a worker agent |
| `swarm_merge_task` | merge completed task back |
| `swarm_finalize` | finish swarm, soft reset with changes staged |
| `swarm_abort` | abort and revert all changes |

## commands

### /swarm

start a multi-agent workflow for complex tasks.

```
/swarm implement user authentication with jwt
```

phases:
1. **init** - saves current git state
2. **clarify** - asks questions if task is ambiguous
3. **plan** - breaks down into parallel subtasks
4. **execute** - spawns workers in parallel, each in isolated worktree
5. **finalize** - merges all changes back

workers automatically get reviewed before completion. if review fails 3 times, worker reports failure.

### /graphite

use graphite cli for stacked PRs.

```
/graphite create a pr for this branch
/graphite submit the stack
```

### /rmslop

remove ai-generated code slop - unnecessary comments, defensive checks, type casts, inconsistent style.

### /swarm-abort

abort current swarm and revert all changes.

### /swarm-status

check status of running swarm.

## knowledge files

### effect.md

effect-ts patterns and best practices. loaded on-demand when working with effect code.

## swarm workflow

for complex multi-file changes:

```
/swarm add rate limiting to all api endpoints
```

swarm will:
- break it into parallel tasks
- spawn workers in isolated worktrees
- review each change
- merge everything back
