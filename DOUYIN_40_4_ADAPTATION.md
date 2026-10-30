# Douyin 40.4.0 experimental adaptation — permanent lock mode

## Static APK findings

- The supplied APK does not define the legacy `com.ss.android.ugc.aweme.video.simplayer.SimPlayer` class.
- `com.ss.android.ugc.aweme.video.PlayerManagerImplA` is present and implements `IPlayerManager`.
- `PlayerManagerImplA` defines `setSpeed(float)`.

## Permanent-lock behavior in this revision

- Hooks `PlayerManagerImplA.setSpeed(float)` in the **before** phase.
- While the Douyin lock switch is enabled, replaces every requested speed with the configured speed before the original method runs.
- Douyin requests to reset playback to 1.0x or another value are intercepted at this method boundary.
- There is deliberately **no automatic re-apply** after video changes, resume, playback preparation, timers, or delayed callbacks.
- Default speed is 2.0x; the existing setting range is 0.25x–4.0x.

## Important limitation

This is an APK-informed static adaptation, not runtime-verified. It assumes the relevant Douyin playback-speed changes pass through `PlayerManagerImplA.setSpeed(float)`. If 40.4.0 changes speed through a lower-level player API without calling this manager method, an additional hook will be required. No installable APK has been built or tested in this environment.
