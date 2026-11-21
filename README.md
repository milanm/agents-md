# My AGENTS.md

This is the cleaned-up version of the rules file I keep in my projects. It has 62 lines.

The working rules come from the rules files in my own projects: what the agent does before a change, during it and after it, what it must never do, and what happens when I correct it. The project lines (commands, paths, class names, decisions) come from a typical .NET API of mine, with the names changed. Replace them with yours.

## How to use it

1. Copy [AGENTS.md](AGENTS.md) to the root of your repo.
2. Replace the commands, the paths and the decisions with your own.
3. Delete every line your agent gets right without it.

Codex, Cursor, GitHub Copilot, Gemini CLI and many other tools read `AGENTS.md`. Claude Code reads it when the project has no `CLAUDE.md` (version 2.1.277 or later). If you keep a `CLAUDE.md`, put one line in it: `@AGENTS.md`.

## Why it is short

Every line has to change what the agent does. Four sources shaped the file.

- **A study from ETH Zurich** tested rules files on real GitHub issues. The files did not raise the success rate, and they raised the cost by more than 20%. The agents did follow the instructions, so every extra requirement made the task harder. The authors advise minimal requirements, written by a human. [Paper](https://arxiv.org/abs/2602.11988)
- **A second study** gave agents a rules file that disagreed with the code. The agents followed the stale file in about 90% of their choices. One sentence that gives the code priority turned that around, and this is why my file has the line "The existing code wins over this file". [Paper](https://arxiv.org/abs/2610.30571)
- **The Claude Code docs** advise a file under 200 lines, with instructions concrete enough to verify. [Docs](https://code.claude.com/docs/en/memory)
- **The Agentic AI Foundation**, which maintains the format, advises exact commands, precise boundaries and pointers to example code. It advises against overviews and generic advice. [Guide](https://aaif.io/blog/writing-an-effective-agents-md)

## What I checked it against

I had Claude read the `AGENTS.md` files of twelve large open-source repos on 21 November 2026, ten of them from Microsoft. Five are behind choices in my file.

- [VS Code](https://github.com/microsoft/vscode/blob/main/AGENTS.md) has 7 lines at the root, and [Roslyn](https://github.com/dotnet/roslyn/blob/main/AGENTS.md) has 23 and calls its file "intentionally thin". Both point to longer files elsewhere in the repo.
- [The Microsoft MCP repo](https://github.com/microsoft/mcp/blob/main/AGENTS.md) puts the fast command for one test class before the full run, and it has an "Ask first" list. My commands and my "Ask first" list follow that.
- [Playwright](https://github.com/microsoft/playwright/blob/main/AGENTS.md) bans agent attribution in commits and pull requests, and it bans a push without an instruction.
- [Azure SDK for .NET](https://github.com/Azure/azure-sdk-for-net/blob/main/AGENTS.md) forbids agents to remove or turn off tests. My line about tests comes from there.

## What I left out

- A project overview and a directory tree. Agents find the files just as fast without them.
- Style rules. The formatter and the analyzers enforce those.
- Advice that fits any project, such as "write clean code".
- Lines the agent wrote by itself. The agent proposes a line, and I decide.

## One warning

An agent treats this file as instructions. Review every change to it the way you review code, and do not start an agent in a folder with an `AGENTS.md` you have not read.

## License

MIT. Copy it, change it, and make it yours.
