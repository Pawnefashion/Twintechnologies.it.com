# Twin Technologies — Zero to AI & Freelance Hero Website

## What's in this folder
- `index.html` — the main landing page (About, Curriculum, Gallery, Pricing, FAQ chat widget)
- `application.html` — the registration/application form
- `assets/` — logo, headshot, and the downloadable curriculum PDF

## Before you go live — 2 things to finish

### 1. Connect the form to Google Sheets
1. Create a Google Sheet with a tab named "Registrations" and these column headers in row 1:
   `Timestamp | Full Name | Email | WhatsApp | Location | Occupation | AI Experience | Motivation | Group Slot | Source | Bank Reference | Payment Status | Confirmation Sent`
2. In the Sheet: **Extensions → Apps Script**, paste this code:

```javascript
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName("Registrations");
  var data = JSON.parse(e.postData.contents);
  sheet.appendRow([
    new Date(),
    data.fullName, data.email, data.whatsapp, data.location,
    data.occupation, data.aiExperience, data.motivation, data.groupSlot,
    data.source, data.bankRef, "Pending", false
  ]);
  return ContentService.createTextOutput(JSON.stringify({status: "success"}))
    .setMimeType(ContentService.MimeType.JSON);
}
```

3. **Deploy → New deployment → Web app**. Execute as "Me", access "Anyone". Deploy and copy the Web App URL.
4. Open `application.html` in a text editor, find this line near the bottom:
   `const GOOGLE_SCRIPT_URL = "PASTE_YOUR_APPS_SCRIPT_URL_HERE";`
   Replace the placeholder text with your actual Web App URL.

### 2. Add your gallery photos
In `index.html`, find the `<div class="gallery-grid">` section. Replace each
`<div class="gallery-item">...</div>` block with:
`<div class="gallery-item"><img src="assets/gallery-1.jpg" alt="Teaching session"></div>`
(adding your photo files into the `assets/` folder as `gallery-1.jpg`, `gallery-2.jpg`, etc.)

## Deploying
1. Push this whole folder to a new GitHub repository.
2. Go to vercel.com → Sign up with GitHub → "Add New Project" → select the repo → Deploy.
3. Under Project Settings → Domains, connect your domain: twintechnologies.it.com