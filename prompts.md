# Prompts

These work with any coding agent. Copy the line in quotes, or the whole block.

## Six prompts for a change

1. **Ask for a plan first.** "Write a plan first, and do not change any code yet." Add your comments, and let the work start only when the plan is right.
2. **Let it ask you.** "Ask me everything you need, and do not guess." Then ask the model what you forgot to ask.
3. **Use a second model.** Give the plan or the result to a model from a different company. "What is wrong with this?"
4. **Review in a fresh session.** A new session never saw the reasoning behind the change, so it does not grade its own work.
5. **Ask for evidence.** "Show me the test output and the command you ran. List every place where you left the plan."
6. **Ask for one more check.** "Check everything once more, and tell me what you left out."

## Review of a change

A fresh session does the review. It gets the plan and the diff, and it never saw the reasoning behind them.

```
Review this change as someone who did not write it.
You have the plan and the diff. Do not change any files.
You may run the build, the tests and any command that only reads.

1. Start with the "Review focus" list in the plan.
2. Check that every requirement is done, that each listed edge case has a test,
   and that nothing outside the task changed.
3. Report only what affects correctness or a stated requirement. Leave style out.
4. For each finding give the file and line, what goes wrong,
   the input or state that shows it, and what it costs if it ships.
5. Mark each finding "ran" or "read". "Ran" means you ran a command and saw it fail,
   so paste the command and its output. "Read" means you traced it in the code.
6. Sort the findings into three lists: fix before release, can wait, fine as it is.
7. List what you did not check.
8. End with a verdict: ship, ship after the fixes, or do not ship.
```

Then comes one fix pass, and every fix starts with a test that fails. The three lists stay in the repo, so the next session knows what was decided.

A reviewer who is asked for problems finds some in sound work too. So I fix the first list and decide on the rest. A finding marked "ran" comes with its proof. A finding marked "read" is a claim, and I check it before I change any code.

## Review of a design

For a design, the reviewer is a model from another company. It reads the design before anything runs for real.

```
Review this design before the first real run.

1. What happens when an input is missing, late, repeated or malformed?
2. Which failure would look like success, for example an empty result?
3. What does it cost per month if one assumption is wrong?
4. What would you cut?

Give the verdict first. Then list what to fix now, what can wait and what to keep as it is.
```

The questions come from one such review in a side project. It found a filter that the service could ignore, one malformed item that could stop the run, and a failed search that looked like "nothing new".

## Before a task that matters

```
Before you start, make my request better.
Tell me what an expert in this field would do here that I did not ask for.
Tell me which original sources they would start from,
and how we can check the result without trusting you or me.
Then rewrite my request and wait for my answer.
```

## One warning

I have not measured these prompts against other wordings. The two review prompts are put together from my plans, my review notes and the sources below.

## Sources

- My own plans and review notes.
- [Best practices for Claude Code](https://code.claude.com/docs/en/best-practices): a reviewer in a fresh context sees only the diff and the criteria. It reports gaps and leaves style out, and not every finding needs a fix.
- [Superpowers](https://github.com/obra/superpowers), the code reviewer template: the file and line, why the finding matters, a clear verdict, and a list of what the reviewer set aside.
- [pstack](https://github.com/cursor/plugins/tree/main/pstack), the `interrogate` skill: a finding that a run proves is worth more than one the reviewer only argues for.
- [Custom Code Review rules for Codex](https://developers.openai.com/blog/custom-code-review-rules-for-codex): a finding names the risk and the rule behind it, and the review rules live in AGENTS.md.
