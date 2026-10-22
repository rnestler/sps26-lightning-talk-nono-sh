---
theme: seriph
title: Put Your Agent in a Box
info: Raphael Nestler — Swiss Python Summit 2026
class: text-center
drawings:
  persist: false
transition: slide-left
# enable Comark Syntax: https://comark.dev/syntax/markdown
comark: true
duration: 5min
---

# Put your agent in a box 📦

…and your `pip install` too. Sandboxing with [nono](https://nono.sh)

<div class="abs-bl m-6 text-sm opacity-70 text-left">
Raphael Nestler · Swiss Python Summit 2026
</div>

<!--
~10s. Hi, I'm Raphael. Five minutes on why I run my coding agent and my
Python tooling in a sandbox, and how easy that is with nono.
-->

---
layout: two-cols-header
---

# Everything runs as *you*

::left::

Claude Code, Cursor, `uv run`, `pip install`, `pytest` …

<v-clicks>

 * 🔑 `~/.ssh`, `~/.aws`, `~/.config/gh`
 * 📄 `.env` in your project
 * 🌍 every `*_TOKEN` in your environment
 * 🗑️ `rm -rf ~`

</v-clicks>

::right::

<v-click>

> LLMs are probabilistic — a <span class="text-red-500">**1%**</span> chance of
> disaster makes it a matter of <span class="text-red-500">*when*</span>, not
> <span class="text-red-500">*if*</span>.
>
> — [agent-safehouse.dev](https://agent-safehouse.dev/)

</v-click>

<!--
~35s. Your agent, and every Python process you start, has the same rights you
have. SSH keys, cloud credentials, the .env file, every token you exported in
your .zshrc. And it can delete your home directory.

An agent doesn't need to be evil. It just has to be wrong once.
-->

---
layout: two-cols-header
---

# It happens

::left::

### 🤖 Agents

<img src="/images/fable-nuked-my-dev-machine.jpg" class="h-70 object-contain" alt="Tweet: Fable nuked my entire dev machine" />

::right::

### 🐍 PyPI

 * **LiteLLM** 1.82.7 / 1.82.8 (Mar 2026)
   * `litellm_init.pth` runs **on every interpreter start**
   * steals env vars, SSH keys, cloud creds, `.env`
 * **Ultralytics** 8.3.41 / 8.3.42 (Dec 2024)
   * cryptominer on install

<!--
~40s. Left: Claude was testing a sandbox it was building itself, by running
rm -rf on the home directory. The sandbox didn't work. Everything gone.

Right: this is the Python part. LiteLLM was backdoored in March. The 1.82.8
release shipped a .pth file. Python executes .pth files at interpreter
startup, so you didn't even need to `import litellm`. Just having it installed
was enough. It was online for about three hours.
Ultralytics in Dec 2024: a cryptominer, also pulled in by ComfyUI.
-->

---

# What doesn't work

<v-clicks>

 * 🙏 **Prompt begging**: "Please don't touch my secrets"
 * 😴 **Approve everything**: approval fatigue, you'll click *yes* anyway
 * 📝 **Agent deny-lists**: they can't cover everything

</v-clicks>

<v-click>

```json
{ "permissions": { "deny": ["Read(.env)"] } }
```

```bash
python -c "print(open('.env').read())"   # 🙃
```

</v-click>

<v-click>

…and none of it helps against a malicious `.pth` file.

</v-click>

<!--
~35s. Asking the model nicely doesn't work. Approving every command doesn't
scale. You'll click yes. Agent permission rules are deny-lists, and Python
alone gives you a dozen ways around them.

And all of this lives inside the agent. A malicious package doesn't care
about your Claude settings.
-->

---

# nono: a sandbox in the kernel

 * **Allow-list** enforced by the OS: Landlock (Linux), Seatbelt (macOS)
 * **Irrevocable**: once applied, not even the sandboxed process can undo it
 * Works for **any command**: agents, `python`, `uv`, `pytest`, …
 * Credentials are **always denied**, even inside allowed paths

```bash
$ nono run --allow-cwd -- python -c "import os; os.listdir('/home/raphael/.ssh')"
PermissionError: [Errno 13] Permission denied: '/home/raphael/.ssh'

$ nono why --profile claude --path ~/.ssh/id_ed25519 --op read
DENIED
  Reason: filesystem_deny
  Details: Path is covered by filesystem.deny rule: /home/raphael/.ssh
```

<!--
~40s. nono uses the same kernel features the OS uses to isolate apps. No
container, no VM, no file syncing. It's your real working copy at native speed.

It's an allow-list: the process only gets what you grant. And once the sandbox
is on, it can't be lifted, not by the agent and not by a malicious package.

`nono why` tells you why something got denied, so you don't have to guess.
-->

---

# For your Python workflow

```bash
# your coding agent, with a ready-made profile
nono run --profile claude -- claude

# the test suite of that PR you're reviewing
nono run --allow-cwd -- uv run pytest

# installing deps: only allow the package index
nono run --allow-cwd \
  --allow-domain pypi.org --allow-domain files.pythonhosted.org \
  -- uv sync
```

<v-click>

 * Undo with atomic snapshots: `nono rollback`
 * Audit trail of what was allowed *and* denied

</v-click>

<!--
~35s. Three ways I use it. The agent with the built-in claude profile. Running
someone else's code, like the tests of a PR. And installing dependencies with
network access limited to PyPI. A stealer can run, but it can't read your
keys and it can't phone home.

Plus: snapshots and rollback if the agent messes up your working copy, and an
audit log.
-->

---
layout: two-cols-header
---

# Don't forget the environment

::left::

Env vars are **inherited by default**

```text
$ export TEST_ENV_TOKEN=my-secret
$ nono run --profile claude -- claude
❯ Show me TEST_ENV_TOKEN
● Bash(echo "$TEST_ENV_TOKEN")
  ⎿  my-secret
```

<v-click>

Better: **credential injection** via proxy, so the agent only ever sees a
phantom token.

</v-click>

::right::

`~/.config/nono/profiles/claude-filter-env.json`

```json
{
  "extends": "claude",
  "environment": {
    "allow_vars": [
      "PATH", "HOME", "TERM",
      "LANG", "LC_*"
    ]
  }
}
```

```text
● Bash(echo "$TEST_ENV_TOKEN")
  ⎿  (No output)
```

<!--
~35s. One gotcha: environment variables are passed through by default. So
that GITHUB_TOKEN in your .zshrc is visible. Fix it with a small profile that
extends the built-in one and allow-lists the variables you need.

Even better: nono can run a proxy that injects the real credential. The agent
only gets a session token that's useless outside the sandbox.
-->

---
class: text-center
---

# P.S. Claude helped me make these slides

…running inside nono:

```text
$ ls ~/projects/python-summit
ls: cannot open directory '/home/raphael/projects/python-summit': Permission denied

$ nono why --self --path /home/raphael/projects/python-summit --op read
DENIED
  Reason: path_not_granted
  Suggested fix: --read /home/raphael/projects/python-summit
```

<div class="mt-8">

**Sandbox as the outer wall + agent permissions + you in the loop**

[nono.sh](https://nono.sh) · [blog: Safe Ways to Use AI Agents](https://blog.rnstlr.ch/safe-ways-to-use-ai-agents.html)

</div>

<!--
~30s. Fun fact: Claude, running in nono, helped me with these slides. It tried
to look one directory up, the sandbox said no, and it told me why.

Takeaway: a sandbox is the outer wall. Keep using the agent's own permissions,
stay in the loop, and the next time a .pth file goes rogue, it's stuck in a
box. Thanks!
-->
