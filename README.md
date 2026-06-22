# Ariston Mobile Game Controller

## Deploy with GitHub Pages

1. Create a GitHub repository and place `index.html`, `Ariston.png`, and this `README.md` in its root.
2. Push the files to the repository's default branch.
3. In GitHub, open **Settings → Pages**.
4. Under **Build and deployment**, choose **Deploy from a branch**, select the default branch and `/ (root)`, then save.
5. Open the Pages URL on the phone. GitHub Pages uses HTTPS, which is supported by Firebase.

## Firebase Realtime Database Rules

The controller writes to `devices/samsung-screen-01/control`. For a quick public demo, the narrowest unauthenticated rules are:

```json
{
  "rules": {
    "devices": {
      "samsung-screen-01": {
        "control": {
          ".read": true,
          ".write": true,
          "horizontal": {
            ".validate": "newData.isNumber() && (newData.val() === -1 || newData.val() === 0 || newData.val() === 1)"
          },
          "start": {
            ".validate": "newData.isBoolean()"
          },
          "$other": {
            ".validate": false
          }
        }
      }
    }
  }
}
```

Publish rules in **Firebase Console → Realtime Database → Rules**. Public writes are suitable only for a controlled demo. For production, enable Firebase Authentication and require an authenticated user in `.write`.
