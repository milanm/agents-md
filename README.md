# My AGENTS.md

This is the cleaned-up version of the rules file I keep in my projects. It has 63 lines.

The working rules come from the rules files in my own projects: what the agent does before a change, during it and after it, what it must never do, and what happens when I correct it. The project lines (commands, paths, class names, decisions) come from a typical .NET API of mine, with the names changed. Replace them with yours.

## How to use it

1. Copy [AGENTS.md](AGENTS.md) to the root of your repo.
2. Replace the commands, the paths and the decisions with your own.
3. Delete every line your agent gets right without it.
4. Move a line into a check when a check can hold it. See [What a check can hold instead](#what-a-check-can-hold-instead).

## Starter kit

Three more files that go with AGENTS.md. They cover one change, from the request to the review.

- [`definition.md`](definition.md): the four lines I write before any task, with what makes each one work and a real example.
- [`plan-template.md`](plan-template.md): the shape of a plan that the agent writes and I comment on. The task steps follow [Superpowers](https://github.com/obra/superpowers). The constraints, the review focus and the last section come from my own plans.
- [`prompts.md`](prompts.md): six prompts for a change, a review prompt for a change and one for a design, and one prompt I use before a task that matters.

The order is: definition, plan, my comments, work, evidence, fresh review.

## Which tools read it

More than twenty tools read `AGENTS.md`. The full list is at [agents.md](https://agents.md), the site of the format. Here is what the common ones need.

- **Codex and Cursor** read `AGENTS.md` with no setup.
- **GitHub Copilot** reads it in the coding agent and in Copilot CLI. Not every Copilot feature supports it yet.
- **Claude Code** (version 2.1.277 or later) reads it when the project has no `CLAUDE.md` or `CLAUDE.local.md`. If you keep a `CLAUDE.md`, put one line in it: `@AGENTS.md`.
- **Gemini CLI** looks for `GEMINI.md` by default. Add this to `.gemini/settings.json`, next to your other settings:

```json
{
  "context": {
    "fileName": ["AGENTS.md", "GEMINI.md"]
  }
}
```

- **Aider** needs one line in `.aider.conf.yml`: `read: AGENTS.md`.

In a monorepo you can put a second `AGENTS.md` in a subproject, such as `client/`. The agent follows the file closest to the code it edits, and what you say in chat overrides every file.

## Why it is short

Every line has to change what the agent does. Four sources shaped the file.

- **A study from ETH Zurich** tested rules files on real GitHub issues. In its September 2026 version, the files did not generally raise the success rate, and the cost went up by more than 20% on average. The agents followed the instructions well, and overviews of the repo did not help them. The authors see such files as useful for practices that are not standard, and they advise measuring any change before you rely on it. [Paper](https://arxiv.org/abs/2602.11988v3)
- **A second study** ran two agents 320 times on 40 Python projects where the rules file disagreed with the code. The agents followed the stale file in about 90% of their choices. One sentence that gives the code priority turned that around. This is why my file tells the agent to follow the existing code for structure, paths and conventions. The test covered conventions only, so my boundaries keep their priority. [Paper](https://arxiv.org/abs/2610.30571)
- **The Claude Code docs** advise a file under 200 lines, with instructions concrete enough to verify. [Docs](https://code.claude.com/docs/en/memory)
- **The Agentic AI Foundation**, which maintains the format, advises exact commands, precise boundaries, pointers to example code and a note on what the structure of the repo means. It advises against directory listings, generic advice and facts the agent can read from the repo itself. [Guide](https://aaif.io/blog/writing-an-effective-agents-md)

## What I checked it against

I had Claude read the `AGENTS.md` files of twelve large open-source repos on 21 November 2026, ten of them from Microsoft. Five are behind choices in my file. The links go to the exact versions that were read.

- [VS Code](https://github.com/microsoft/vscode/blob/abe19dbe42d4b2de282593e245b6636bf324817f/AGENTS.md) has 7 lines at the root, and [Roslyn](https://github.com/dotnet/roslyn/blob/5fd9ae81fa37bc5c2e8c2de2d171c70e5b796fd8/AGENTS.md) has 23 and calls its file "intentionally thin". Both point to longer files elsewhere in the repo.
- [The Microsoft MCP repo](https://github.com/microsoft/mcp/blob/731c14497b796a2912e7226edfdcc23c18703f16/AGENTS.md) puts the fast command for one test class before the full run, and it has an "Ask first" list. My commands and my "Ask first" list follow that.
- [Playwright](https://github.com/microsoft/playwright/blob/b7cc538524d6b4b1c3eb0450e350e4306c0f5ed1/AGENTS.md) bans agent attribution in commits and pull requests, and it bans a push without an instruction.
- [Azure SDK for .NET](https://github.com/Azure/azure-sdk-for-net/blob/5efe0a777637db02c5e71dafa301a76d19cc474b/AGENTS.md) forbids agents to remove or turn off tests unless a person asks for it. My line about tests comes from there.

## What I left out

- A project overview. The site of the format lists it among the suggested sections. I left it out because repo overviews did not help the agents in the ETH tests.
- A directory tree and facts the agent can read from the repo itself.
- Style rules. The formatter and the analyzers enforce those.
- Advice that fits any project, such as "write clean code".
- Lines the agent wrote by itself. The agent proposes a line, and I decide.

## What a check can hold instead

An agent can skip a line in this file and nothing fails. A check fails every time the rule is broken. So when I correct an agent, the fix goes to the first of these that can hold it: the design, a type, an analyzer or CI check whose error names the fix, a test, and only then a line here.

Three lines in my file have a check that can take over.

| Line in AGENTS.md | Check |
|---|---|
| Package versions live in `Directory.Packages.props`, never in a `.csproj`. | Central Package Management. A version in a `.csproj` fails the restore with [NU1008](https://learn.microsoft.com/nuget/reference/errors-and-warnings/nu1008), and the error says where the version belongs. |
| Use `DateTime.UtcNow`, never `DateTime.Now`. | [BannedApiAnalyzers](https://github.com/dotnet/roslyn/blob/main/src/RoslynAnalyzers/Microsoft.CodeAnalysis.BannedApiAnalyzers/BannedApiAnalyzers.Help.md). Put `P:System.DateTime.Now;Use DateTime.UtcNow` in `BannedSymbols.txt` and set RS0030 as an error. |
| `appsettings.*.local.json` and `secrets.json` stay out of git. | `.gitignore` for the two names, and [push protection](https://docs.github.com/en/code-security/concepts/secret-security/push-protection) on GitHub for secrets in a known format. |

A line leaves the file once its check runs in CI. The other lines stay as text because they are judgment calls. A check cannot tell that a test was weakened to get a green run.

The order comes from the `correct` skill in [pstack](https://github.com/cursor/plugins/tree/main/pstack) by Lauren Tan.

## Two warnings

An agent treats this file as instructions. Review every change to it the way you review code, and do not start an agent in a folder with an `AGENTS.md` you have not read.

Nobody has measured this file on my own tasks. The studies above explain its shape. They do not prove that it makes an agent better in your repo, so measure it there.

## License

MIT. Copy it, change it, and make it yours.
