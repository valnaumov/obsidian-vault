---
Created: 2024-03-08T12:10
tags:
  - Meeting-Log
Updated: 2024-03-08T13:12
---
# Preparation
## What was done
Last month from 2024-01-23 (inclusive) to 2024-02-23 (exclusive).
- Fixing StorageUtil to store data outside of app dir
    - Remove unused libs from www
    - Sort the contents of www by feature
        - Change form.ftl templates
    - Remove bat file, use npm script (cross-platform), clear intentions.
    - Fix NPEs in ReportUtil
    - Refactor StorageUtil to use Java NIO
    - Fix Archive to ZIP (used to package the folder that’s a parent of the project, not the project folder itself).
- jpackager
    - Checking it on linux
    - Using a secondary launcher
    - Jx browser back and forth: keys, DPI scaling, updated public api
- Updating java
    - Upgrading Mockito library,
What was done concerning the issues mentioned on the previous call: