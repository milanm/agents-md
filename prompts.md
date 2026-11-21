# Prompts

These work with any coding agent. Copy the line in quotes.

## Six prompts for a change

1. **Ask for a plan first.** "Write a plan first, and do not change any code yet." Add your comments, and let the work start only when the plan is right.
2. **Let it ask you.** "Ask me everything you need, and do not guess." Then ask the model what you forgot to ask.
3. **Use a second model.** Give the plan or the result to a model from a different company. "What is wrong with this?"
4. **Review in a fresh session.** A new session never saw the reasoning behind the change, so it does not grade its own work.
5. **Ask for evidence.** "Show me the test output and the command you ran. List every place where you left the plan."
6. **Ask for one more check.** "Check everything once more, and tell me what you left out."

## The review prompt for the second model

Paste the plan or the diff under it.

```
Review this as someone who did not write it.
Start with the "Review focus" list if the plan has one.
For each problem, give the file and line, what goes wrong, and the input that shows it.
Separate what is wrong from what you would only do differently.
Finish with what you did not check.
```

## Before a task that matters

```
Before you start, make my request better.
Tell me what an expert in this field would do here that I did not ask for.
Tell me which original sources they would start from,
and how we can check the result without trusting you or me.
Then rewrite my request and wait for my answer.
```
