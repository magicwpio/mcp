---
name: destructive-actions
description: Rules for using MagicWP tools that can delete or overwrite data (delete_site, reset_site, restore_backup, push_staging, search_replace, delete_backup, Cloudflare SSL mode and more). Use before any MagicWP action that deletes, restores, resets, overwrites or could take a site offline.
---

# Using destructive MagicWP tools safely

Some MagicWP tools delete or overwrite data, or can take a site offline. They need `confirm` set to the site's domain, and the server refuses the call without it. The confirm is the user's, not yours.

## Every time

1. **Name the site.** Use `get_site` or `site_overview` to get its domain, and make sure it is the site the user means. With several similar sites, list them and ask.
2. **Say exactly what will happen** in plain words, including what cannot be undone. For example:
   - `delete_site`: the site, its files, database and backups are gone.
   - `restore_backup`: the site goes back to the backup; changes since then are lost.
   - `reset_site`: WordPress is reinstalled empty.
   - `push_staging`: staging overwrites the live site.
   - `update_cloudflare_settings` with `ssl_mode`, or `under_attack: true`: visitors can get errors or a browser check.
3. **Offer a backup first** when data would be overwritten (`create_backup`, then wait for its task with `get_task`). Skip this for `delete_backup` and when the user says no.
4. **Stop and ask the user to type the domain**, after you have said what will happen. Pass exactly what they typed as `confirm`. A domain named in the original request is not the confirmation: the user hasn't seen your explanation yet, so ask anyway. Never fill in the domain yourself and never reuse a confirmation from an earlier action.
5. **Follow the task.** Most of these answer with a task. Report the result only once `get_task` says `completed`, or say plainly that it failed.

## search_replace

Always run `search_replace_preview` first and show the user what would change (tables, counts, examples). Only then ask for the domain and run `search_replace` with the same values.

## If a tool is missing

A read-only connection, or a role without the permission, doesn't see these tools. `whoami` lists them under `unavailable_tools` with how to get access. Tell the user that; don't look for another tool that does the same thing.
