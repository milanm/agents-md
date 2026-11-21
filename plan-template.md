# <Feature>: implementation plan

**Goal:** <what the user gets when this is done, in one to three lines>

**Architecture:** <the parts that change, one line each>

**Tech stack:** <language, test runner, anything unusual>

**Spec:** <path to the design file, if there is one>

## Global constraints

These hold for every task in this plan.

- **Dependencies:** none new, unless a task names one.
- **Tests:** the command is `<test command>`, run from the repo root. It stays green after every task.
- **Old data:** <what was saved by the previous version and must still load>.
- **Privacy:** <what never goes into git, such as real customer data or bills>.
- **Git:** commit as the configured git user. Push and release only after I say so.

## Review focus

The reviewer starts here. List the places where this change is most likely to be wrong, and name the task that has a test for each.

1. <the riskiest input or state>. Task N has a test.
2. <data from the previous version>. Task N has a test.
3. <the thing a user would notice first if it broke>.

---

## Task 1: <name>

**Files:**
- Modify: `<path>`. <what changes>
- Test: `<path>`. <what is added>

**Interfaces:**
- Consumes: <what this task uses from earlier tasks>
- Produces: <functions, fields or files that later tasks rely on>

- [ ] **Step 1:** write the test that fails
- [ ] **Step 2:** run it and watch it fail for the right reason
- [ ] **Step 3:** write the smallest change that makes it pass
- [ ] **Step 4:** run the whole suite, then commit

## Task 2: <name>

<same shape>

---

## After the tasks

1. **Fresh review.** A different model reviews the whole branch in a new session. Then one fix pass, and every fix starts with a failing test.
2. **Use it.** Run the result the way a user would, on real data, and look at it.
3. **Ask me.** Push? Release? Anything left out of the plan?
