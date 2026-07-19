# Setup Git Committer

A GitHub Action that configures Git committer identity for automated commits.

## Usage

### Basic

```yaml
- uses: ganeshkrishnareddy/setup-git-committer@v1
```

### Custom Identity

```yaml
- uses: ganeshkrishnareddy/setup-git-committer@v1
  with:
    name: 'Your Name'
    email: 'you@example.com'
```

### With Push Token

```yaml
- uses: ganeshkrishnareddy/setup-git-committer@v1
  with:
    name: 'Deploy Bot'
    email: 'bot@example.com'
    token: ${{ secrets.GITHUB_TOKEN }}

- run: |
    git add .
    git commit -m "chore: update build"
    git push
```

### Auto Commit Changes

```yaml
steps:
  - uses: actions/checkout@v4
  
  - uses: ganeshkrishnareddy/setup-git-committer@v1
    with:
      name: 'github-actions[bot]'
      email: 'github-actions[bot]@users.noreply.github.com'
  
  - run: |
      echo "changes" >> file.txt
      git add .
      git commit -m "chore: automated update"
      git push
```

## Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `name` | No | `github-actions[bot]` | Git committer name |
| `email` | No | `github-actions[bot]@users.noreply.github.com` | Git committer email |
| `token` | No | `''` | GitHub token for push auth |

## What It Does

1. Sets `user.name` and `user.email` globally
2. Configures sensible defaults (`init.defaultBranch`, `pull.rebase`, `core.autocrlf`)
3. Optionally sets up token-based push authentication

## License

MIT
