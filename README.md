# Claw Machine Mobile Controller

This phone controller writes to Firebase Realtime Database at:

`machines/red-blue-01/control`

It provides held Up, Down, Left, and Right controls plus one-shot Drop and Open actions. Open `index.html` through an HTTPS web host such as GitHub Pages; do not open it directly as a local file.

## Firebase rules for a controlled demo

```json
{
  "rules": {
    "machines": {
      "red-blue-01": {
        "control": {
          ".read": true,
          ".write": true,
          "$direction": {
            ".validate": "$direction.matches(/^(up|down|left|right)$/) && newData.isBoolean()"
          },
          "dropCommand": { ".validate": "newData.isNumber()" },
          "openCommand": { ".validate": "newData.isNumber()" }
        }
      }
    }
  }
}
```

Public writes should only be used for a supervised demo. Production deployments should enable Firebase Authentication and require an authenticated controller.

## Run locally

From this directory, run `python -m http.server 8765`, then open `http://localhost:8765`.
