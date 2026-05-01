# Grawin GitHub Pages

This repository hosts public pages for Grawin apps through GitHub Pages.

## Pages

- `/` - App index page.
- `/signal-sense-privacy/` - Signal Sense privacy policy used for Google Play and in-app privacy links.

## When to Update Signal Sense Privacy Policy

Update `signal-sense-privacy/index.html` whenever Signal Sense changes any user-visible privacy, permission, data collection, data sharing, or retention behavior.

Common triggers:

- A new Android permission is added or removed.
- A permission starts being used for a new purpose.
- Location, phone/SIM, Wi-Fi, Bluetooth, notification, account, or identifier access changes.
- Background Monitoring behavior changes, including when it starts, what it logs, how long it runs, notification behavior, or retention.
- Signal log fields change, especially location, SSID/BSSID, phone number/MSISDN, IMSI, ICCID, IMEI, carrier, subscription ID, or cell identifiers.
- Export, share, clipboard, backup, sync, upload, or deletion behavior changes.
- Firebase Analytics, Crashlytics, Performance Monitoring, or any other third-party SDK is added, removed, enabled by default, or starts receiving different event/context data.
- Default telemetry settings change.
- Data retention changes, including the 24-hour auto-purge behavior for Background Monitoring logs.
- Play Console Data Safety answers change.
- In-app disclosure text changes materially.

## Policy Consistency Checklist

Before publishing app updates, compare these files and keep them consistent:

- Signal Sense app disclosures in `app/src/main/res/values*/strings.xml`.
- Signal Sense README privacy/permissions section in the app repository.
- This hosted policy at `signal-sense-privacy/index.html`.
- Google Play Console Data Safety form.
- Google Play Console permission declarations, especially Location, Foreground Service Location, Phone, Nearby Wi-Fi Devices, and Notifications.

For Signal Sense specifically, the policy should continue to state:

- Normal app use shows live diagnostics while the user is using the app.
- Continuous signal history is collected only when the user turns on Background Monitoring.
- Background Monitoring runs as a foreground service with a persistent notification.
- Signal logs and coordinates stay local by default.
- User exports/shares are user initiated.
- Optional Firebase telemetry is controlled by the user.
- Signal logs, coordinates, phone numbers, and SIM/device identifiers are not intentionally attached to Firebase analytics events.
- Signal Sense does not request `ACCESS_BACKGROUND_LOCATION`.

## Validation

This is a static HTML site. Before committing changes:

```bash
git diff --check
python3 - <<'PY'
from html.parser import HTMLParser
from pathlib import Path

for path in Path('.').glob('**/*.html'):
    parser = HTMLParser()
    parser.feed(path.read_text())
    parser.close()
    print(f'ok {path}')
PY
```

If editing visible HTML text, check that literal ampersands are escaped as `&amp;` and angle brackets in text are escaped as `&lt;` or `&gt;`.
