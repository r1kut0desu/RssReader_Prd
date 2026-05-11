# RssReader_Prd

SideStore distribution source for the personal RssReader iOS app.

This repository contains the compiled IPA + SideStore source manifest only.
The actual Swift source code is kept private at `~/claude_workspace/tools/RssReader`.

## Setup (one-time, iPhone)

1. Open SideStore on iPhone
2. Settings → Sources → Add Source
3. Paste this URL:
   ```
   https://raw.githubusercontent.com/r1kut0desu/RssReader_Prd/main/apps.json
   ```
4. RssReader appears in Sources tab → tap "Get" → SideStore signs + installs

Or use the deep link (open in Safari on iPhone):
```
sidestore://source?url=https://raw.githubusercontent.com/r1kut0desu/RssReader_Prd/main/apps.json
```

## Update flow (each release)

On Mac:
```bash
~/claude_workspace/tools/RssReader/update.sh
```

The script:
1. Builds an unsigned IPA from the Swift source
2. Copies it into this repo
3. Bumps `version` and `buildVersion` in `apps.json`
4. Commits and pushes

On iPhone (auto if Auto Update is enabled in SideStore Settings):
1. SideStore polls this source periodically
2. Detects new version, downloads, re-signs, installs

If Auto Update is OFF, the user manually opens SideStore Sources tab and taps "Update".

## Caveats

- GitHub raw URL has a small CDN cache (~5 min). Updates may take a few minutes to propagate.
- LocalDevVPN must be connected for SideStore to perform the re-sign step.
- This is a personal distribution channel. IPA is unsigned; anyone can download but they'd need their own Apple ID for SideStore to sign it for them.
