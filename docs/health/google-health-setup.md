# Google Health API Setup

This guide covers a general Google Health API project and the exact read profile used by this dashboard for a Fitbit Inspire 2. Google changes Cloud Console labels and layouts periodically, so the guide names both the current section and the underlying concept.

Official references: [Google Health setup](https://developers.google.com/health/setup), [scope catalog](https://developers.google.com/health/scopes), and [developer checklist](https://developers.google.com/health/developer-checklist).

## 1. Link The Health Account First

Before OAuth, sign into the Google Health mobile app with the Google Account that owns the health profile. Existing Fitbit users must complete Fitbit-to-Google account migration when prompted. OAuth can authenticate an ordinary Google Account even when it has no linked Google Health profile, which later produces `ACCOUNT_NOT_LINKED` errors.

## 2. Create And Select A Cloud Project

1. Open [Google Health setup](https://developers.google.com/health/setup).
2. Use **Enable the API and get an OAuth 2.0 Client ID**, or open Google Cloud Console manually.
3. Create a project, or select a development project that is not used for production.
4. Confirm the selected project in the project picker before every later step.
5. In **APIs & Services > Library**, search for **Google Health API** and select **Enable**.

The quick setup may use slightly different wording. The required outcome is a selected Cloud project with Google Health API enabled.

## 3. Configure Google Auth Platform

Open **Google Auth Platform** for the same project.

### Branding

Provide an application name, support email, and developer contact email. A local personal project does not need public marketing content, but required fields must be complete.

### Audience

1. Choose **External** unless the account belongs to a managed organization that requires **Internal**.
2. Leave publishing status as **Testing** during local development.
3. Under **Test users**, choose **Add users** and add every Google Account that will authorize the app.

The current console may save each test-user row immediately and show only a trash icon; there may be no separate page-level Save button. Navigate away and return to confirm that the row remains.

Testing-mode refresh tokens generally expire after seven days. Production publication changes token behavior but introduces policy and verification obligations.

### Data Access

1. Select **Add or remove scopes**.
2. Filter the API column for **Google Health API**.
3. Select only the scopes required by the application.
4. Choose **Update**, then **Save** on the Data Access page when that action is present.

Scope selection controls what the user may consent to; it does not guarantee that a particular device generated that data.

## 4. Choose Scopes By Capability

Use product features and intended application behavior, not brand name alone.

| Intended data or operation | Scope | Typical source |
| --- | --- | --- |
| Steps, distance, activity level, exercise, active minutes | `googlehealth.activity_and_fitness.readonly` | Phone tracking, Fitbit trackers, Pixel Watch, compatible wearables |
| Heart rate, oxygen saturation, respiratory metrics, temperature, weight | `googlehealth.health_metrics_and_measurements.readonly` | Sensor-equipped wearables, scales, or manual records |
| Sleep sessions and stages | `googlehealth.sleep.readonly` | Sleep-capable wearable or manually logged sleep |
| Exercise GPS traces | `googlehealth.location.readonly` | Built-in or phone-assisted GPS during recorded exercise |
| Basic profile | `googlehealth.profile.readonly` | Google Health account |
| Units, timezone, stride, and paired-device metadata | `googlehealth.settings.readonly` | Google Health account and paired devices |
| ECG | `googlehealth.ecg.readonly` | Explicitly ECG-capable products only |
| Irregular Rhythm Notifications | `googlehealth.irn.readonly` | Eligible product, firmware, country, account, and enabled feature |
| Nutrition | `googlehealth.nutrition.readonly` | Logged account data; not inferred from wearable hardware |

A newer release year is not enough to infer ECG, GPS, temperature, or IRN support; verify the product specification and inspect `users/me/pairedDevices` after authorization.

Useful rough expectations:

- A basic tracker or phone source usually supports activity and fitness.
- A continuous-heart-rate wearable often justifies health metrics and sleep.
- GPS location requires recorded exercise location from either the wearable or its paired phone.
- ECG and IRN should be treated as explicit product, firmware, and regional capabilities, never as generic smartwatch features.
- Nutrition, symptoms, mindfulness, and reproductive-health data are account logging features, not capabilities implied by a wrist device.

## 5. Inspire 2 Profile Used Here

### Required For The Current Dashboard

```text
https://www.googleapis.com/auth/googlehealth.activity_and_fitness.readonly
https://www.googleapis.com/auth/googlehealth.health_metrics_and_measurements.readonly
https://www.googleapis.com/auth/googlehealth.sleep.readonly
https://www.googleapis.com/auth/googlehealth.profile.readonly
https://www.googleapis.com/auth/googlehealth.settings.readonly
```

These cover movement, steps, exercise, heart-rate and related measurements, sleep, account profile, units, battery level, device model, and last synchronization time.

### Optional For Inspire 2

```text
https://www.googleapis.com/auth/googlehealth.location.readonly
https://www.googleapis.com/auth/googlehealth.irn.readonly
```

- **Location** is useful only when an exercise has a GPS trace, including phone-assisted GPS.
- **IRN** is useful only when Irregular Rhythm Notifications are available and enabled. [Google lists Inspire 2 support](https://support.google.com/googlehealth/answer/14236719) at firmware `44.1.124.34` or newer, subject to eligibility and regional availability.

Nutrition, ECG, reproductive health, mindfulness, and symptom scopes do not become useful merely because an Inspire 2 is paired.

## 6. Create The OAuth Client

Open **Google Auth Platform > Clients > Create client**.

1. Choose **Web application**.
2. Give it a recognizable local-development name.
3. Under **Authorized JavaScript origins**, either leave the list empty or enter only:

   ```text
   http://127.0.0.1:8917
   ```

4. Under **Authorized redirect URIs**, enter the complete callback:

   ```text
   http://127.0.0.1:8917/callback
   ```

5. Create the client.

Do not put `/callback` in **Authorized JavaScript origins**. Origins cannot contain a path and produce: `Invalid Origin: URIs must not contain a path or end with "/".` The callback belongs under **Authorized redirect URIs**.

## 7. Store The Client JSON Privately

Save the OAuth client as:

```text
secrets/google_health_client.json
```

The `secrets/` directory is ignored by Git. Never place this file in `docs/`, `config/`, or a commit.

If the console offers **Download JSON**, use it. Depending on the console version, the action may appear immediately after creation, inside the client detail page, behind the client name, or beside the edit action.

If no download action is available, create the file manually using the displayed client ID and secret:

```json
{
  "web": {
    "client_id": "REPLACE_WITH_CLIENT_ID",
    "client_secret": "REPLACE_WITH_CLIENT_SECRET",
    "auth_uri": "https://accounts.google.com/o/oauth2/auth",
    "token_uri": "https://oauth2.googleapis.com/token",
    "redirect_uris": [
      "http://127.0.0.1:8917/callback"
    ]
  }
}
```

## 8. Authorize And Verify

Run:

```powershell
node scripts/google_health_oauth.mjs
```

The helper opens the system browser, requests offline access, receives the localhost callback, stores tokens under ignored `secrets/`, and verifies identity and paired-device access.

Use the same Google Account that appears under **Audience > Test users**. During testing, Google may show an unverified-app warning; review the project name and requested scopes before continuing.

Successful authorization creates private local files and reports paired devices. Then run:

```powershell
node scripts/google_health_sync.mjs
```

## 9. Common Failures

| Symptom | Cause and fix |
| --- | --- |
| Clicking the documentation setup button appears to do nothing | Open Cloud Console directly, confirm the selected project, then enable Google Health API in the API Library. |
| No application-type choices appear | Finish Branding and Audience, then open **Clients > Create client**. |
| `Invalid Origin` mentions a path | Move the localhost callback from JavaScript origins to Authorized redirect URIs. |
| Test user is called ineligible | Confirm the address is a Google Account, retry the row, and verify that it persists after navigation. |
| `Required parameter is missing: response_type` | Do not open a partial OAuth URL manually; run the OAuth helper, which constructs the full request. |
| `redirect_uri_mismatch` | The URI in the client and JSON must exactly equal `http://127.0.0.1:8917/callback`. |
| `ACCOUNT_NOT_LINKED` | Sign into the Google Health mobile app and create or migrate the health profile before OAuth. |
| A data type is empty | The device or account may not produce it, the feature may be disabled, or the required scope was not granted. |
| Refresh stops after about seven days | Testing-mode refresh tokens are time-limited; reauthorize or review production requirements. |
