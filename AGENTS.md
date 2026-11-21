# AGENTS.md

## Commands

- Build: `dotnet build`
- One test class: `dotnet test --filter "FullyQualifiedName~OrderServiceTests"`
- All tests: `dotnet test`
- Client tests: `npm test`, run from `client/`

Run one test class while you work, and the full suite before you report. Stop the running API before a build, or the build fails on a locked DLL.

## Before you write code

- Ask before you write code when two readings of the request would lead to different results.
- Write a plan and wait for my approval when a change touches the public API, the database schema, authentication or the architecture, or more than 3 files. The plan goes to `docs/plans/YYYY-MM-DD-<topic>.md`.
- Copy the pattern of the closest existing feature. `OrdersController`, `OrderService` and `OrderServiceTests` are the reference set.
- For structure, paths and conventions, follow the existing code over this file, and tell me where they disagree. The boundaries below always hold.

## While you write code

- Make the smallest change that solves the task. Leave nearby code as it is: no refactoring, no extra features, no cleanup.
- Change an existing file before you create a new one.
- Fix a bug in two steps. First write a test that fails because of the bug, then change the code until it passes.

## Done means

- The build and the tests pass, and you ran them in this session. Report each command and its result.
- New behavior has a unit test. A change that crosses the API, the database or another service also has an integration test.
- You listed the edge cases the change adds, and the test that covers each one.
- If the change had a plan, you said where you left it, and why.
- You said what you did not verify.

## Boundaries

Never:

- Commit a secret. `appsettings.*.local.json` and `secrets.json` stay out of git.
- Call a live third-party API or use a production secret in a test. Use the fakes in `tests/Fakes/`.
- Delete, skip or weaken a test to get a green run.
- Edit generated code (`*.g.cs`, `Migrations/*.Designer.cs`). Change the source and generate it again.
- Add a `Co-Authored-By` trailer or a "Generated with" footer to a commit or a pull request. Commit as the configured git user.

Ask first:

- Before you delete a file, or discard changes you did not make.
- Before you add a NuGet or npm package.
- Before you change `global.json`, `NuGet.config`, `Directory.Build.props`, `.editorconfig` or `.github/workflows/*`.
- Before you push, force-push or amend a commit.
- Before you create a cloud resource or do anything else that costs money.

## Decisions already made

Do not reopen these without a concrete reason.

- Controllers call services directly. No CQRS, no MediatR, no repository layer.
- One API and one database. No docker-compose and no Aspire.
- Package versions live in `Directory.Packages.props`, never in a `.csproj`.
- Timestamps are UTC. Use `DateTime.UtcNow`, never `DateTime.Now`.

## When I correct you

Find the root cause and propose one line for this file. I decide whether it goes in.
