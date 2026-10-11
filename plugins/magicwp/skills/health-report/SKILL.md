---
name: health-report
description: Build a read-only health report for all MagicWP sites in the workspace - uptime, pending updates, backups, PHP and WordPress versions, disk use. Use when the user asks how their sites are doing, for a portfolio or status report, or what needs attention.
---

# MagicWP portfolio health report

A read-only check of every site in the workspace. It changes nothing, so it works with a read-only connection too. Tools that the connection can't use are listed by `whoami` under `unavailable_tools`: skip those columns and say which ones were skipped and why.

## Gather

1. `whoami`: the workspace name, for the report title.
2. `list_sites`: every site. Leave out sites that are still being built or deleted, and list them separately.
3. For each site, read what you need. With many sites, start with the essentials and ask before going deeper:
   - `site_overview`: one call with the details (PHP and WordPress versions, disk quota), whether the front page answers over HTTPS, pending updates, the latest backups and current resource use.
   - `wp_core_check`: whether a newer WordPress release is available.
   - Only when something looks off: `check_site_up` for a second look, `site_metrics` with `daily` for disk and traffic trends.

## Report

Start with one line: how many sites, how many need attention.

Then a table, one row per site, worst first:

| Site | Up | WordPress | PHP | Updates | Last backup | Disk |
|------|----|-----------|-----|---------|-------------|------|

Flag a site when:
- it is down, or answers with an error;
- a security update is pending;
- WordPress is a major version behind;
- the PHP version is older than 8.2;
- there is no successful backup in the last 7 days;
- disk use is over 85% of the quota.

End with a short list of what to do, most urgent first, naming the tool for each (for example "Run updates on shop.example.com with manage_updates"). Don't run any of it unless the user asks; for anything destructive, follow the destructive-actions skill.
