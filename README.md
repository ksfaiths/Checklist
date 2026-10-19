# Eclipse's Astral Quest Log

A small galaxy-themed daily checklist for Lioden with private cloud sync between iPad and iPhone.

## What's included
- `index.html` — website, matching the Lioden colors/gradients and all 9 original daily tasks.
- `config.js` — two public Supabase connection settings you fill in.
- `schema.sql` — secure database table and row-level security policies.

## Setup (one time)
1. Create a project at https://supabase.com/dashboard (a free plan may be available; verify current limits). Save your project database password privately.
2. Open **SQL Editor** in Supabase, paste the entire `schema.sql`, and run it **once**. This creates the `quest_checks` table and privacy rules.
3. Open **Project Settings → API Keys** (location/names may vary). Find the **Project URL** and **publishable key** (or older **anon** key). Add both strings to `config.js`. NEVER use the **service_role** / **secret** key here.
4. Upload `index.html` and `config.js` to a new GitHub repository, along with `README.md` if you want. Don't upload any passwords.
5. In the GitHub repository, go to **Settings → Pages**, set deployment to **Deploy from a branch**, `main`, root `/`, and save. GitHub will give you a public website URL, usually `https://YOURNAME.github.io/REPOSITORY/`.
6. In Supabase, go to **Authentication → URL Configuration**. Set the Site URL to the published GitHub Pages URL and add the exact published URL as an allowed redirect URL. The email login link must redirect back to the site.
7. In Supabase **Authentication → Providers**, ensure Email sign-in is enabled. For email OTP, the default email template may send a magic link; the site handles either a link or a numeric code (when the template sends `{{ .Token }}`). Check your Supabase email quota and template if no email arrives.
8. Open the hosted website on iPad, sign in with your email. Open the SAME website on iPhone and sign in with the SAME email. Task changes save to the database and refresh on both devices (the other device checks approximately every 12 seconds while the page is active, or when you return to the tab).
9. In Lioden's Territory Description, link to your site:

```html
<a href="https://YOURNAME.github.io/REPOSITORY/" target="_blank" rel="noopener noreferrer">✧ Open Astral Quest Log ✧</a>
```

## Important details
- **Not yet online:** These files are an installable website package, not a deployed URL. Until you configure a Supabase project and deploy to GitHub Pages, no cross-device cloud sync is possible.
- **Privacy:** The website URL can be public, but tasks are per authenticated user. The SQL Row Level Security (RLS) policies restrict read/write to the signed-in user. Never put Supabase secrets/service-role key in frontend files.
- **Sessions:** Each device signs in using the same email; browsers normally remember the session unless site data is cleared or cookies/storage are restricted.
- **Sign-in emails:** Supabase's free default email sending has rate limits. You may need a custom SMTP provider for heavy use.
- **Sync delay:** The site saves immediately when you click. Other devices update after a short polling interval; refresh / switch tabs to update sooner.
- **Reset:** "Reset all tasks" asks for confirmation and clears the stored checkmarks across all devices.
- **Custom tasks:** To change the labels, edit the `TASKS` array near the bottom of `index.html`. Keep the task IDs stable to preserve your saved progress. New task IDs start unchecked.
- **Checking locally:** You may preview the styling when config is missing. The preview explicitly does not save or sync.
- **Embedding:** Lioden descriptions generally cannot embed working third-party apps via CSS alone. Linking to the hosted checklist is the reliable approach.
