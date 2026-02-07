# stacklite-mentor
Design Philosophy

The agent is built around four core principles:

1. Debugger First

The debugger is the source of truth. Code changes are blocked until runtime behavior is inspected and explained.

2. Understanding-Gated Progress

The agent will not proceed unless the user can explain:

--What the code is doing?

--Why it behaves that way--

--What assumptions were incorrect?

--Perfect wording is not required. Correct mental models are.

3. Teaching as Proof of Understanding

Users are often asked to “explain it to a junior developer.”
If you can teach it clearly, you understand it.

4. Momentum Without Frustration

A controlled Bail Mode exists to prevent deadlock while preserving learning intent.

🛠️ Key Features
IDE-Aware Entry Gate

Every session starts by asking which IDE the user is using.

Current support:

Visual Studio (C# / .NET)

The architecture is designed to extend to PyCharm and other IDEs.

Visual Studio Debugging Coverage

The agent actively teaches and enforces use of:

Breakpoints and conditional breakpoints

Step Over / Step Into / Step Out

Locals, Autos, and Watch windows

Call stack and stack frame inspection

Exception settings

Async debugging with Tasks and Parallel Stacks

Tool locations are only explained when asked or when the user is blocked, encouraging IDE fluency instead of hand-holding.

Understanding Gate

Before continuing, the user must explain the concept being used.

Examples:

What the call stack represents

Why a breakpoint triggers

How state changes across method calls

How async execution resumes

Partial understanding gets one clarification attempt.
Repeated confusion triggers Bail Mode.

Bail Mode (Safety Valve)

Bail Mode prevents infinite loops when a learner is stuck.

When activated, the agent:

Temporarily relaxes the understanding gate

Provides a concise explanation

Walks through the runtime behavior step-by-step

Requires the user to re-explain the concept

Once re-explained, gated learning resumes.

Explain-It-to-a-Junior Mode

To verify real understanding, the agent frequently asks users to explain concepts as if mentoring a junior developer.

This enforces:

Plain language

Cause-and-effect reasoning

Practical examples

Failure to explain correctly is logged for later review.

Misunderstanding Logging

When:

Bail Mode is triggered, or

Understanding gates fail repeatedly

The agent logs:

The misunderstood concept

The debugging context

The observed misconception

These logs can later drive:

Review sessions

Targeted debugging drills

Reinforcement practice

 Debugging Drills

The agent includes intentionally deceptive debugging drills designed to surface common misconceptions.

Drills often:

1. Look at the code level 

2. Behave unexpectedly at runtime

3. Require call stack or state inspection

4. Trigger Bail Mode naturally

--The goal is to teach why the debugger matters.--

Technical Implementation

Platform: Claude Code

Configuration: YAML-based agent definition

Model: Claude Haiku

Tool Restrictions:

Write and Edit tools disabled

Hooks:

Block code changes until the debugger reasoning is provided

Behavior is enforced structurally, not just conversationally.
