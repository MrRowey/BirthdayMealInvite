# Birthday Meal Invite 🎂

A free, mobile-friendly birthday RSVP website built with GitHub Pages and Google Sheets / Apps Script.

## Event

- **Date:** Saturday 20 February 2027
- **Time:** 6:00 PM
- **Venue:** The Red Lion, Shrewsbury, UK (confirm which Red Lion before adding its exact address).
- **Gift preference:** No presents; a contribution towards the meal is appreciated instead, so everyone can enjoy the evening.

## Features

- Personalised invitation URL for each guest or household
- RSVP Yes / Maybe / No, number attending, dietary requirements and a message
- Guests can update responses using their original link
- Host dashboard with invitation creation, link copying, response table and summary counts
- All response data lives in your private Google Sheet

## One-time Google setup

1. In your Google Drive, create a Google Sheet named **Birthday Meal RSVPs**.
2. Go to **Extensions > Apps Script** in that spreadsheet. Replace the default Code.gs contents with [apps-script/Code.gs](apps-script/Code.gs).
3. Select **setup** in the Apps Script function dropdown and click **Run**. Approve Google permissions. Open **Execution log** and copy the long **host access code**. Keep it private. The code is also stored as the ADMIN_KEY script property.
4. In Apps Script, click **Deploy > New deployment > Web app**. Set **Execute as: Me** and **Who has access: Anyone**. Authorise and deploy. Copy the Web app URL ending in /exec. This is required for guests without Google accounts. Keep the spreadsheet private; it is not shared with guests.
5. Edit **config.js** in GitHub: paste the Web app URL into **apiUrl** (inside quotes).
6. Make the GitHub repository **public** (GitHub Pages on GitHub Free requires a public repository). Under **Settings > Pages** choose **Deploy from a branch**, branch **Develop**, folder **/(root)**, then Save.
7. Visit **https://mrrowey.github.io/BirthdayMealInvite/admin.html**, enter your host code, and create a test invitation. Open its generated personal link in a private browser tab, RSVP and verify the dashboard.

### Security and limitations

- **Never** add the host code to the GitHub repo or invitation URL. Enter it manually in the dashboard. Keep the Google Sheet private.
- Each personal invite URL is a **bearer link**: anyone with it can view/edit that invitation. Share only with the intended guest. There are no guest passwords.
- Host code protects the dashboard API, but this lightweight design is **not suitable for sensitive/private information**. Host actions use JSONP GET requests; URLs (including the host code and RSVP notes) can appear in browser/service logs, and GET requests can be replayed. For stronger privacy, replace this approach with authenticated POST requests via a more robust backend. Do not collect sensitive medical details.
- Google Apps Script has usage quotas. This design suits a small, personal event, not a high-traffic public service.
- If the invitation link was leaked, create a fresh guest entry, and delete the old row from the Sheet.
- The dashboard refreshes when you click **Load dashboard**, rather than updating in realtime.
- Don't assume the restaurant address without confirming the branch: multiple pubs called Red Lion exist in the Shrewsbury area.

## Configuration

Change event details in **config.js**. Both pages use the same Google Apps Script endpoint. No frontend build step, npm, or paid service is needed.
