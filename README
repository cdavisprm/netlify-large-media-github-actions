# Install

This is a Node.js project so be sure to run `npm install` after cloning.

Copy `.env.example` to `.env` and populate the secrets with yours.

Finally, install [`nektos/act`](https://github.com/nektos/act) to run locally, if you like. You can do that once installed with `npm run action`.

# Problem

Netlify Deploy Previews cannot be generated in Github Actions if using Large Media.

Large Media files are not downloaded during the Github Actions checkout process so they are missing on the Deploy Preview link.

# Solution

Large Media is typically configured for the very first time in the local shell with the following commands:

```sh
netlify link
netlify lm:setup
netlify lm:install
source $HOME/.bashrc
```

However, in the case of environments like Github Actions, Large Media is already configured, and there are already many files to download. That looks like this:

```sh
netlify lm:install
source $HOME/.bashrc
git lfs fetch
git lfs checkout
```

I created a Github Actions workflow that does this and it works locally on my machines when using [`nektos/act`](https://github.com/nektos/act).

However, once deployed to Actions itself there is an error:

```
Run export SHELL=/usr/bin/bash
export SHELL=/usr/bin/bash
npx netlify lm:install
source $HOME/.config/netlify/helper/path.bash.inc
git lfs fetch
git lfs checkout
shell: /usr/bin/bash -e {0}
env:
NODE_OPTIONS: --max_old_space_size=4096
NETLIFY_AUTH_TOKEN: ***
NETLIFY_SITE_ID: ***
[02:24:28] Checking Git version [started]
[02:24:28] Checking Git version [2.34.1] [title changed]
[02:24:28] Checking Git version [2.34.1] [completed]
[02:24:28] Checking Git LFS version [started]
[02:24:28] Checking Git LFS version [3.0.2] [title changed]
[02:24:28] Checking Git LFS version [3.0.2] [completed]
[02:24:28] Checking Git LFS filters [started]
[02:24:28] Checking Git LFS filters [completed]
[02:24:28] Installing Netlify's Git Credential Helper for Linux [started]
[02:24:28] Installing Netlify's Git Credential Helper for Linux [completed]
[02:24:28] Configuring Git to use Netlify's Git Credential Helper [started]
[02:24:28] Configuring Git to use Netlify's Git Credential Helper [completed]
┌───────────────────────────────────────────────────────────────────────┐
│ │
│ Run this command to use Netlify Large Media in your current shell │
│ │
│ source /home/runner/.config/netlify/helper/path.bash.inc │
│ │
└───────────────────────────────────────────────────────────────────────┘
fetch: Fetching reference refs/heads/main
fatal: could not read Username for 'https://***.netlify.app': No such device or address
batch response: Git credentials for https://***.netlify.app/.netlify/large-media not found.
error: failed to fetch some objects from 'https://***.netlify.app/.netlify/large-media'
```

