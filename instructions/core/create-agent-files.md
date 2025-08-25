---
description: AI Agent File Generation Rules for Agent OS
globs:
alwaysApply: false
version: 1.0
encoding: UTF-8
---

# AI Agent File Generation Rules

## Overview

Generate configuration files for various AI coding agents based on the project's standards and product information.

<pre_flight_check>
  EXECUTE: @.agent-os/instructions/meta/pre-flight.md
</pre_flight_check>

<process_flow>

<step number="1" subagent="context-fetcher" name="context_gathering">

### Step 1: Context Gathering

Use the context-fetcher subagent to read the following files to understand the project's standards, tech stack, and mission.

<files_to_read>
  - @.agent-os/standards/tech-stack.md
  - @.agent-os/standards/code-style.md
  - @.agent-os/standards/best-practices.md
  - @.agent-os/product/mission.md (if it exists)
  - @.agent-os/product/tech-stack.md (if it exists, it overrides the global one)
</files_to_read>

</step>

<step number="2" subagent="file-creator" name="create_agents_md">

### Step 2: Create AGENTS.md

Use the file-creator subagent to create the file: `AGENTS.md`. The content should be a summary of the project's setup, code style, and testing instructions.

<file_template>
# AGENTS.md

This file provides instructions for AI coding agents working on this project.

## Project Overview

{{mission}}

## Setup commands
- Install deps: `{{install_command}}`
- Start dev server: `{{start_command}}`
- Run tests: `{{test_command}}`

## Code style
{{code_style}}

## Best Practices
{{best_practices}}

</file_template>

</step>

<step number="3" subagent="file-creator" name="create_clinerules">

### Step 3: Create .clinerules

Use the file-creator subagent to create the file: `.clinerules`. The content should provide project-specific instructions for the Cline coding agent.

<file_template>
# .clinerules

## Project Overview
{{mission}}

## Tech Stack
{{tech_stack}}

## Coding Standards
{{code_style}}
{{best_practices}}

</file_template>

</step>

<step number="4" subagent="file-creator" name="create_qoder_rules">

### Step 4: Create .qoder/rules

Use the file-creator subagent to create the file: `.qoder/rules`. This file will contain rules to constrain the Qoder AI's output.

<file_template>
# .qoder/rules

## Global Rules
- Follow the coding style defined in the project's `standards/code-style.md`.
- Adhere to the best practices outlined in `standards/best-practices.md`.
- Use the project's tech stack as defined in `product/tech-stack.md`.

</file_template>

</step>

<step number="5" subagent="file-creator" name="create_roocode_instructions">

### Step 5: Create RooCode Instructions

Use the file-creator subagent to create the file: `.roocode/instructions.md`. This file will contain custom instructions for the RooCode agent.

<file_template>
# RooCode Custom Instructions

## About the Project
{{mission}}

## Key Technologies
{{tech_stack}}

## Development Guidelines
- **Code Style**: Please adhere to the following code style guidelines:
{{code_style}}

- **Best Practices**: Please follow these best practices:
{{best_practices}}

</file_template>

</step>

<step number="6" name="user_notification">

### Step 6: User Notification

Inform the user that the agent configuration files have been created.

<notification_message>
I have created the following AI agent configuration files:

- `AGENTS.md`
- `.clinerules`
- `.qoder/rules`
- `.roocode/instructions.md`

You can review these files to see the project-specific instructions for each agent.
</notification_message>

</step>

</process_flow>

<post_flight_check>
  EXECUTE: @.agent-os/instructions/meta/post-flight.md
</post_flight_check>
