---
Created: 2023-11-14T00:35
"Issue #": 3
Updated: 2023-11-14T00:46
---
Setting `--force-device-scale-factor=1` switch on Chromium seems to fix the issue. Also, the issue is not present when display scaling is set to 100% in Windows.
Gotta test with a different page, because it could be the CSS values that are somehow bound to screen resolution.