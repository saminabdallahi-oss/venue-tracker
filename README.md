# Venue Tracker

A password-protected wedding venue dashboard connected to Google Sheets via Apps Script.

## Files

| File | Purpose |
|------|---------|
| `index.html` | The main dashboard — do not edit unless changing layout |
| `config.js` | Your password and Apps Script URL — edit this file only |
| `README.md` | This guide |

---

## Changing the password

Open `config.js` and update the `password` value:

```js
const CONFIG = {
  password: "your-new-password",
  apiUrl: "https://script.google.com/macros/s/..."
};
```

Commit and push the change to GitHub. The new password takes effect immediately.

---

## Changing the Apps Script URL

If you redeploy your Apps Script and get a new URL, update `apiUrl` in `config.js` the same way.

---

## Hosting on GitHub Pages

1. Create a new repository on GitHub (can be private)
2. Upload all three files (`index.html`, `config.js`, `README.md`)
3. Go to **Settings → Pages**
4. Set source to **Deploy from a branch → main → / (root)**
5. Hit Save — your site will be live at `https://yourusername.github.io/repo-name`

---

## Giving someone access

Since the site is password protected, just share the URL and the password with them directly. No GitHub account needed on their end.

To revoke access: change the password in `config.js`, commit, and push. Their session will expire on next visit.

---

## Google Sheets structure

The connected Sheet must have two tabs named exactly:
- `Domestic`
- `International`

Both tabs use these columns in order (row 1 = headers):

| A | B | C | D | E | F | G | H | I | J | K |
|---|---|---|---|---|---|---|---|---|---|---|
| venueName | town | capacity | airportCode | distanceFromAirport | onSiteLodging | lodgingInfo | pricePerDay | projectedTotalCost | whatsIncluded | status |

Valid status values: `Considering`, `Shortlisted`, `Visited`, `Booked`, `Rejected`

---

## Apps Script (backend)

The Apps Script is deployed as a Web App from within the Google Sheet:
- **Execute as:** Me
- **Who has access:** Anyone

It handles `GET` (read all venues) and `POST` (add / update / delete a venue).

To update the script: paste new code in Extensions → Apps Script, then **Deploy → New deployment** and update the URL in `config.js`.
