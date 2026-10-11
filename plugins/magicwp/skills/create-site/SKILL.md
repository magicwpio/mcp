---
name: create-site
description: Create a new MagicWP WordPress site safely and wait for it to finish building. Use when the user asks to create, launch, spin up or clone a WordPress site on MagicWP.
---

# Create a MagicWP site and wait for it

Building a site is a background task. `create_site` and `clone_site` answer at once with the new site and a task id; the site is **not ready** until that task completes.

## Before creating

1. Call `whoami` to see the workspace and that the connection can create sites. If `create_site` is in `unavailable_tools`, tell the user what it says under `how_to_get_access` and stop.
2. Call `catalog` with `what: limits` and read `can_create`. If it is false, tell the user why (the site limit of their plan) and stop. Don't try anyway.
3. If the user didn't say, ask for what matters to them and leave the rest to the defaults:
   - a label (5 to 15 characters),
   - the region (`catalog` with `what: regions`),
   - a template (`catalog` with `what: templates`), if they want to start from one.
4. Repeat back what will be created in one line and go ahead once the user agrees. Creating a site uses one of the plan's site slots.

## Create and wait

1. Call `create_site` (or `clone_site` to copy an existing site). Keep the `site_id` and the task id.
2. Tell the user the site is being built and which step it is on (`progress`).
3. Call `get_task` with the task id and `wait_seconds: 60`. A build usually takes about a minute, longer from a template or for a clone. If it is still running, say which step it is on and call `get_task` again. Don't poll faster than this.
4. When the task is `completed`, call `check_site_up` for the new site and give the user its address and the wp-admin link. Offer `magic_login` if they want to sign in.
5. When the task is `failed`, say so plainly with the task's error. Don't retry on your own; ask the user first.

## Don't

- Don't call the site live, open its front page or read its WordPress version before the task is `completed`.
- Don't create a second site because the first one is "taking long". Check the task instead.
- Don't make up a domain. Base domains come from `catalog`; custom domains are added later with `manage_domain`.
