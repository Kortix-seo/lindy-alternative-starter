# lindy-alternative-starter: an open-source Kortix example you own

Kortix is the open-source CompanyOS: your agents, their skills, your company memory, and every connector live in one git repo you own, and each session runs on its own cloud computer. This repository is a small, runnable example built on it: one agent that triages a shared inbox, plus the files that govern it and run it. Read the code and point the agent at the work your team hands over.

The repository also shows the shape of an owned system. `kortix.yaml` at the root declares the agent, its connectors, and its schedule. `agents/inbox-triage.md` holds the agent's behavior. One cron trigger runs the agent on weekday mornings. The agent reads the inbox, classifies what it finds, drafts replies, files follow-ups, and opens a change request so a person reviews the work before it lands.

## What is in this repository

- `kortix.yaml`: the manifest. It declares the `inbox-triage` agent, the `gmail` and `linear` connectors, and one cron trigger.
- `agents/inbox-triage.md`: the agent's behavior, as a markdown file with frontmatter and a prompt.
- `examples/run.sh`: starts one inbox-triage session.
- `docs/what-you-own.md`: the files in the repo, the self-host path, the model keys, and the change-request gate.
- `docs/lindy-vs-owned-kortix.md`: the short comparison with Lindy.

## Quickstart

Install the CLI, sign in, and ship the project. The install script runs on macOS and Linux, and on Windows inside WSL.

```sh
curl -fsSL https://kortix.com/install | bash
kortix login

git clone https://github.com/<your-org>/lindy-alternative-starter
cd lindy-alternative-starter
kortix ship
```

`kortix ship` validates `kortix.yaml`, commits the files, asks for any missing secrets, pushes the branch, and offers to connect the declared connectors. Then run the agent for one session:

```sh
kortix sessions new --agent inbox-triage \
  --prompt "Triage the shared inbox now: classify each new thread, draft replies, and open a change request with a summary." \
  --wait
```

The session clones the repo onto its own branch, does the work, commits, and opens a change request. Review and merge it yourself:

```sh
kortix cr ls
kortix cr diff 1
kortix cr merge 1
```

A session runs one agent in its own sandbox on a new branch, named for the session id. The `inbox-triage` agent has no merge grant, so its change requests wait for a person. To move the whole system onto infrastructure you control, the `kortix self-host` command family installs and runs the full stack. Run it on Kortix Cloud, in your VPC, or on your own on-prem network, and self-host is free.

## Start

The same files run on the managed cloud and on your own machines. Try Kortix at [kortix.com](https://kortix.com), read the [Kortix docs](https://kortix.com/docs), or browse [Kortix on GitHub](https://github.com/kortix-ai/suna).

This example supports the comparison at [lindyalternative.com](https://lindyalternative.com). The page that sorts the options by what you own is [lindyalternative.com/lindy-alternatives](https://lindyalternative.com/lindy-alternatives).

The jobs this example takes over are set out on [lindyalternative.com/lindy-use-cases](https://lindyalternative.com/lindy-use-cases), and the cost comparison is on [is Lindy worth it](https://lindyalternative.com/is-lindy-worth-it).
