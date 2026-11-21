# The definition of a task

Four lines. I write them before the agent starts, and they go at the top of the request.

1. **What I need**, in one sentence.
2. **Who it is for.**
3. **The limits**, such as budget, time and what must not change.
4. **How we will know that the result is good.**

## What makes each line work

- **What I need.** Say the result, and leave the solution to the plan. If one sentence is not enough, it is probably two tasks.
- **Who it is for.** Name a real user and what they do with the result.
- **The limits.** Three kinds: what must not change, what is out of scope, and what needs my yes first. Out of scope matters most, because the agent guesses when the request is silent.
- **How we will know.** A check that returns pass or fail: a test, a build, a number that must match. Add one check on real data, from start to finish. Two people who read the line should agree on whether it passed.

## Before the work starts

Two prompts find what the four lines missed.

```
Ask me one question at a time about anything that is unclear.
Start with the questions whose answer would change the design.
```

```
What did I not ask that I should have?
```

## Example

From [aztree 0.4.0](https://github.com/milanm/aztree/compare/v0.3.0...v0.4.0), a tool that shows an Azure bill as a map.

1. **What I need:** the bill split by one tag, Azure's forecast for the month, and a list of resources that cost money while they do nothing.
2. **Who it is for:** anyone who pays an Azure bill and wants to see where the money went.
3. **The limits:** no new dependencies. The page loads nothing from the network. Data saved by the previous version must still open. Real billing data never goes into git. Out of scope: the .NET port, and anything that changes the existing views. Push and release only after I say so.
4. **How we will know:** the tests stay green after every task. On a real bill, the tag total equals the service total to the cent.

For a small fix, lines 1 and 4 are enough.

## Sources

- My own design files and plans. The example is from one of them.
- [Best practices for Claude Code](https://code.claude.com/docs/en/best-practices): a check the agent can run, an interview before a larger feature, and a spec that says what is out of scope and ends with one end-to-end check.
- [A field guide to finding your unknowns](https://claude.com/resources/articles/a-field-guide-to-claude-fable-finding-your-unknowns): one question at a time, starting with the ones that change the architecture, and a pass for what you did not think to ask.
- [How to write a good spec for AI agents](https://addyosmani.com/blog/good-spec/), by Addy Osmani: the user, the need and the success criteria come first, and the limits come in three tiers.
