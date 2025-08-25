---
description: Add a new AI provider to Agent OS
globs:
alwaysApply: false
version: 1.0
encoding: UTF-8
---

# Add New Provider Rules

## Overview

This instruction adds a new AI provider to the Agent OS configuration.

<pre_flight_check>
  EXECUTE: @.agent-os/instructions/meta/pre-flight.md
</pre_flight_check>

<process_flow>

<step number="1" name="get_provider_name">

### Step 1: Get Provider Name

Prompt the user to enter the name of the new provider. The name should be a single word in lowercase, for example, `openai`.

<user_prompt>
Please enter the name for the new provider (e.g., openai, gemini):
</user_prompt>

</step>

<step number="2" subagent="file-creator" name="create_provider_directory">

### Step 2: Create Provider Directory

Use the file-creator subagent to create a new directory for the provider. The directory name should be in the format `<provider_name>-code`.

<directory_to_create>
{{provider_name}}-code/agents
</directory_to_create>

</step>

<step number="3" subagent="file-creator" name="create_placeholder_agents">

### Step 3: Create Placeholder Agent Files

Use the file-creator subagent to create placeholder files for the new provider's agents.

<files_to_create>
  - {{provider_name}}-code/agents/context-fetcher.md
  - {{provider_name}}-code/agents/date-checker.md
  - {{provider_name}}-code/agents/file-creator.md
  - {{provider_name}}-code/agents/git-workflow.md
  - {{provider_name}}-code/agents/project-manager.md
  - {{provider_name}}-code/agents/test-runner.md
</files_to_create>

<file_content>
# {{agent_name}} Agent

This is a placeholder for the {{agent_name}} agent for the {{provider_name}} provider.
You should edit this file to provide the specific instructions for this agent.
</file_content>

</step>

<step number="4" name="update_config">

### Step 4: Update config.yml

Update the `config.yml` file to add the new provider to the `agents` list and enable it.

<file_to_update>
config.yml
</file_to_update>

<update_logic>
Append the following to the `agents` section in `config.yml`:

  {{provider_name}}_code:
    enabled: true
</update_logic>

</step>

<step number="5" name="user_notification">

### Step 5: User Notification

Inform the user that the new provider has been added.

<notification_message>
I have added the new provider: {{provider_name}}.

A new directory has been created at `{{provider_name}}-code` with placeholder agent files.
You should now edit these files to provide the specific instructions for the new provider's agents.

The provider has been enabled in `config.yml`.
</notification_message>

</step>

</process_flow>

<post_flight_check>
  EXECUTE: @.agent-os/instructions/meta/post-flight.md
</post_flight_check>
