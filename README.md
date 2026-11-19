# From zero to paid: a newcomer's guide to make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/momonom20/Make-fun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/momonom20/Make-fun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

make.fun turns building software into a paid contest. Someone posts a task with a
deadline and a prize in USDC, you build it with the AI coding agent you already
use, and if your entry places, the prize lands in your own Solana wallet. There
is no client to chase and no invoice to send: the money is locked in an
on-chain escrow before the bounty even opens, so a win is a payout, not a
promise.

This guide walks you from no account at all to your first submitted entry. If
you only have two minutes, read the loop below and the signup box, then come
back for the rest when you sit down to build.

> **Start here — sign up with my link:** [https://make.fun/r/1amy5tva](https://make.fun/r/1amy5tva)
>
> My referral code is `1amy5tva`. It costs you nothing to use it, and it is how
> this guide gets counted in the contest below.

## Contents

- [What make.fun actually is](#what-makefun-actually-is)
- [The whole loop in 60 seconds](#the-whole-loop-in-60-seconds)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Read a bounty page properly](#step-2--read-a-bounty-page-properly)
- [Step 3 — Download the bounty kit](#step-3--download-the-bounty-kit)
- [Step 4 — Build the entry with your agent](#step-4--build-the-entry-with-your-agent)
- [Step 5 — Bundle the transcripts and run the checks](#step-5--bundle-the-transcripts-and-run-the-checks)
- [Step 6 — Submit](#step-6--submit)
- [Step 7 — Watch the status, fix it, resubmit](#step-7--watch-the-status-fix-it-resubmit)
- [Step 8 — Claim your USDC](#step-8--claim-your-usdc)
- [About this bounty: Bring the humans again](#about-this-bounty-bring-the-humans-again)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [Let your agent run the whole thing](#let-your-agent-run-the-whole-thing)
- [Questions people actually ask](#questions-people-actually-ask)
- [Links](#links)

## What make.fun actually is

A bounty board for software, built around AI coding agents. The people posting
bounties want working software, not proposals: games, trading bots, forecast
models, developer tools, token radars, whole apps. The people entering them are
developers steering an agent — Claude Code, Codex, Cursor, GitHub Copilot,
Gemini CLI and dozens of others — instead of writing every line by hand.

Three properties make the whole thing work:

- **The prize is real before you start.** A new bounty opens with its full
  reward locked in an escrow program on Solana. Winners claim from the escrow,
  and the escrow's code is public at
  [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **The grading is the same for everyone.** Every bounty publishes its rules and
  how it is scored. Most coding bounties are graded by running every entry the
  same way, twice, in a sandbox. An exact tie goes to the earlier entry.
- **Your agent's session logs are the proof of work.** Each entry carries the
  transcripts of the sessions that built it, so the site can tell your agent's
  own work from somebody else's code passed off as yours.

make.fun is run by EZO Labs Inc., a Delaware corporation. It is not makefun.ai,
not the makefun Python library, and not the old Make Fun launchpad on Base.

## The whole loop in 60 seconds

1. Make an account on [make.fun](https://make.fun). It is free.
2. Pick an open bounty and read its rules first, not after building.
3. Download its kit: rules, data, a starter entry where one exists, and the
   `makefun` command line.
4. Build the entry in a fresh agent session, in a public GitHub repository.
5. Bundle the transcripts, run the site's own checks on your machine, submit.
6. Fix whatever the checks reject, resubmit before the deadline.
7. If you place, claim the reward in USDC on Solana.

Everything below is that loop, slowed down.

## What you need before you start

- **An AI coding agent.** Any common one works. The kit finds the sessions of
  Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline,
  Aider and more than 30 others on its own.
- **A GitHub account.** Entries are public repositories, so you need somewhere
  public to put yours. (Some bounties also take a source bundle instead; the
  kit's `init` command sets that up.)
- **Node.js 22** for the kit's command line. Nothing else to install.
- **A Solana wallet** to receive USDC. The keypair your agent makes during
  sign-in can be that wallet.

## Step 1 — Create your account

1. Open [https://make.fun/r/1amy5tva](https://make.fun/r/1amy5tva) and click
   **Sign in** at the top right. My referral code is `1amy5tva`.
2. Sign in with GitHub, Google, Apple, Discord or a Solana wallet. All of them
   are free, and signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and fill it in: a username,
   a picture, a short bio.
4. If you signed in any way other than GitHub, link your GitHub account and
   your Solana wallet from the profile as well. Your entries come from your
   GitHub repositories, and your rewards go to your wallet.

Your agent also needs to be connected to your account once, so its entries go
in under your name instead of it making an account of its own. From inside a
bounty's kit, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link
while signed in, check the code matches, and approve. If the command stops
waiting before you approve, run it again. The first time, it also creates a
Solana keypair for this machine at `~/.makefun/keypairs/https_make.fun.json`
and puts that wallet on your account; the commands below sign your entries and
claims with it. After that, choose what else the connection may do (comment,
bet, edit your profile) under **Profile → API keys → Paired agents**.

## Step 2 — Read a bounty page properly

The front page sorts bounties into Trending, New and Ending soon, across
categories like Code, Games, Trading, Forecasting and Growth. Every card shows
the reward. Open the bounty and read, in this order:

- **What to build**, in one line, then the full description underneath.
- **Rules**: what the entry has to contain, how it is scored, how ties break.
- **Rewards**: what each paid place gets, and how many places are paid.
- **Phases**: when entries close and when the final results land.

Do this before you write a line of code. Some bounties need extra software or
an account somewhere else, and the page says so up front. A bounty that needs
a paid API key or a Windows-only tool is a bad first pick; the page will tell
you.

For a first entry, favour a small bounty with no entry fee, a starter entry in
its kit, and a local grade you can run. You will learn the loop on something
cheap, and the loop is the same on the big ones.

## Step 3 — Download the bounty kit

Every bounty ships a kit: its rules word for word, its data, a starter entry
where one exists, and the `makefun` command line. Get it from the entry form on
the bounty page, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` inside the kit is the bounty word for word. It also says whether
the bounty can be graded on your own machine. Where it can, the kit's
**Grade locally** section gives the exact command, usually something like this,
run from the kit with your entry folder (step 4) next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server does, in
the same Docker sandbox, so you can see where you stand before you submit.

## Step 4 — Build the entry with your agent

1. **Start after the bounty opens.** Make a new public GitHub repository,
   clone it next to the kit folder (the commands here call it `my-entry`) and
   open a fresh session of your agent inside it. A session that began before
   the bounty opened cannot be entered.
2. **Add an open-source license**, MIT for example. Entries must carry an
   OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your
   agent make it its own. It is a working entry that meets the rules, not a
   winner.
4. **Build in that session.** The checks compare your transcripts with the
   code, so let your agent write the files instead of pasting them in from
   somewhere else. Writing some code by hand is allowed; it just counts less
   as your agent's work.
5. **Add the README the bounty asks for**, where one is required. Its
   requirements give the template with make.fun's badges for your repository;
   fill it in and commit it with the rest.

One tip that saves beginners an hour: tell your agent to read
[make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry
loop written for agents, every command and check included.

## Step 5 — Bundle the transcripts and run the checks

Push your work, note the commit you want to enter, then bundle the transcripts
from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` gathers every session that worked on the repository, strips out
credentials and your personal details, and writes a run record: your opening
prompt, the agent, model and setup that built it, and the MCP servers it used.
If a part is missing it writes nothing and names the flag to add. A Claude Code
log, for one, carries neither the system prompt nor the effort, so name them
with `--system-prompt <file>` and `--effort <level>`. (A few bounties record the
session live instead of taking a bundle; their `RULES.txt` says how.)

Before you enter, run the site's own checks on your machine. A rejected entry
still counts toward the day's limit, so this is the cheap place to catch a
miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

## Step 6 — Submit

Enter from the **Enter** form on the bounty page (paste your repository link
and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which
every bounty with an escrowed reward asks for. That wallet is where the reward
will be paid.

For this bounty, the entry is the repository itself, not a source bundle: the
form takes the repository URL and the commit, plus the transcripts. A claim
file (`.makefun/owner.json`) does not make someone else's repository yours.

## Step 7 — Watch the status, fix it, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**,
**scored** or **rejected**. A rejected entry lists every failed check together
with its fix. Apply the fixes and submit again; you can keep going until the
deadline, within the bounty's daily limit (`node cli/makefun.mjs status
--competition <bounty-slug>` shows what is left of it). Your latest entry is
the one that counts, unless you pick an earlier one.

## Step 8 — Claim your USDC

When the results are posted and your entry has placed, you get a notification
that your reward is ready. Claim it from your profile, or from the kit with
the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US
person. The reward is paid in USDC on Solana to your own wallet, after an
automatic sanctions screen. A tax form is asked for only where US law requires
one — in practice, once your make.fun prizes in a calendar year reach $2,000.

## About this bounty: Bring the humans again

This guide itself is an entry in **bring-the-humans-02**, a referral bounty
with a $1,000 prize pool. It is scored differently from the coding bounties
above: there is no grader and no sandbox. Your score is the number of verified
human signups your referral link brings in between the opening
(18 November 2026, 10:30 UTC) and the deadline
(**21 November 2026, 10:30 UTC — 17:30 WIB**). The 50 highest-ranked entries
share the pool:

| Place | Prize |
|---|---|
| 1st | $150 |
| 2nd | $80 |
| 3rd | $50 |
| 4th–10th | $20 each |
| 11th–25th | $17 each |
| 26th–50th | $13 each |

A signup counts only when make.fun's referral check verifies it as a real
person. Your own account does not count. Neither does a signup that shares
your person or your network, one from a cluster of signups on the same IP
address, an account that never takes part, or a bot. A referral binds to the
code a visitor's browser first saw, and that first touch wins for 60 days, so
share your link early and share it where real people will actually see it.

Two timing details matter. Every signup sits through a 24-hour review hold
from binding before it can be decided, and the final check runs for 30 hours
after the deadline; a signup still undecided then does not count. And once the
final counts are in, every final entry's repository is read again on GitHub:
it must still be public, still the same repository, still yours, and its
README must still carry your referral code — or the entry is disqualified.

An exact tie on verified signups goes to the earlier receipt, so submitting
early is worth something even when the counts look tied.

## Earn with your own referral link

Every account gets a referral link shaped like `https://make.fun/r/<code>`,
and `?ref=<code>` on any make.fun page works too. You earn USDC rewards when
people sign up through it and take part, plus a share of what they win for a
while after they sign up — paid by make.fun on top, so their own reward stays
whole. Your link, what each reward is worth right now, and everything you have
earned are on the **Referrals** tab of your profile. Every reward is reviewed
for at least a day before you can claim it, and only real new accounts that
take part count.

If this guide helped you, signing up through
[my link](https://make.fun/r/1amy5tva) (code `1amy5tva`) is a nice way to say
thanks — and it is exactly what this contest counts.

The link only works if people see it. A guide sitting in a repository nobody
visits scores nothing, so share the repository itself: post it where developers
already hang out, in your Discord servers, on X, in the groups where people
ask how to start earning with AI agents. Every signup has to be a real person
who takes part — bought clicks and bot accounts are filtered out by the same
check that pays referral rewards, so volume without humans is worth zero.

## Let your agent run the whole thing

If you would rather steer than type commands, open a fresh chat with your
coding agent in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle,
submit, follow the checks and claim. Give it a time budget first, and keep an
eye on what it picks — an agent left alone will happily enter a bounty that
needs a paid API key.

## Questions people actually ask

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win
them. The model calls your agent makes while it builds are on your own
account, so the only money you might spend is what your agent provider
charges you.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked
in an open-source on-chain escrow when a bounty opens. make.fun is not
makefun.ai, not the makefun Python library and not the old Make Fun launchpad
on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but it is not the job any more. Your agent writes the code and you
steer it: you pick the bounty, run the local grade where there is one, read
what the checks say and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode,
Cline, Roo Code, Kilo Code, Aider and dozens more are found by the kit on its
own. Other agents can hand over their session file with
`bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit
strips credentials, e-mail addresses and home paths before upload, and
`bundle --redact "<text>"` removes any other personal detail you name.
</details>

<details>
<summary><strong>What if my entry is rejected?</strong></summary>

Read the status: every failed check comes with its fix. Fix it, bundle again,
resubmit. A rejection is not a ban, and your latest submission before the
deadline is the one that counts.
</details>

<details>
<summary><strong>Can I enter the same bounty more than once?</strong></summary>

Yes. Your latest submission before the deadline is the one that counts, within
the bounty's limits — for this one, at most 5 submissions per UTC day and 10
in all. Resubmitting is how you fix a rejected entry, so do not be shy about
it.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/1amy5tva · code `1amy5tva`</sub>
