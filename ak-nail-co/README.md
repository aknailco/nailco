# AK Nail Co website: owner guide

## What's in this folder

| File | What it is |
|---|---|
| `index.html` | Your shop website |
| `admin.html` | Your owner dashboard (add, edit and delete sets, change prices, upload photos) |
| `products.json` | The product list the website shows when no database is connected |
| `config.json` | Where you paste your Supabase keys (step 4 below) |
| `supabase-setup.sql` | One-time database setup script (step 3 below) |
| `img/` | The 51 original product photos |

Upload **the whole folder** to your hosting. Keep all the files together.

Your dashboard is at `https://your-website.com/admin.html`. There's also a small **Owner login** link at the bottom of the website.

---

## Option A: Supabase (recommended, free)

Once this is set up, you can log in from your phone, upload photos and change prices, and the website updates right away. You won't need to touch any code. The setup takes about 10 minutes and you only do it once.

### 1. Create a free account
Go to **supabase.com** and click **Start your project**. Sign up with Google or email.

### 2. Create a project
Click **New project** and fill in:
- **Name:** `ak-nail-co`
- **Database password:** anything strong. Save it somewhere safe.
- **Region:** pick the one closest to Pakistan (for example Mumbai or Singapore).

Click **Create** and wait about 2 minutes.

### 3. Run the setup script
1. Open `supabase-setup.sql` in Notepad.
2. On the **last line**, change `your-email@example.com` to the email you'll log in with.
3. In Supabase, open **SQL Editor** from the left menu and click **New query**.
4. Paste the whole file and click **Run**. You should see "Success".

### 4. Connect your website
1. In Supabase, open **Project Settings** (the gear icon), then **API** (it may be called **API Keys** or **Data API**).
2. Copy the **Project URL** and the **anon public** key. Newer projects call this the **Publishable** key.
3. Open `config.json` in Notepad and paste them between the quotes:

```json
{
  "supabaseUrl": "https://abcdxyz.supabase.co",
  "supabaseAnonKey": "eyJhbGciOi...your long key...",
  "storageBucket": "nail-images"
}
```

4. Save the file and upload it to your hosting, replacing the old one.

> The anon or publishable key is meant to be public, so it's safe to have it on your website. **Never** paste the `service_role` or **Secret** key anywhere.

### 5. Create your login
1. In Supabase, go to **Authentication**, then **Users**, then **Add user**, then **Create new user**.
2. Enter **the same email you put in step 3** and choose a password.
3. Tick **Auto Confirm User** and click **Create**.
4. Then go to **Authentication**, then **Sign In / Providers** (or **Settings**), and **turn off "Allow new users to sign up"**. Only you need an account.
5. (Optional, for "Forgot password") Go to **Authentication**, then **URL Configuration**. Set **Site URL** to your website address, and add `https://your-website.com/admin.html` under Redirect URLs.

### 6. First login
1. Open `your-website.com/admin.html` and sign in.
2. The product list will be empty. Click **Import the starter collection** to load all 51 current sets into your database.

You're done. From now on, everything happens in the dashboard.

---

## Using the dashboard

| To do this | Do this |
|---|---|
| **Add a new set** | Click **Add new set**, add photos (tap or drag), type a name and price, choose a style and shape, then click **Save set**. New sets appear at the top of the website. |
| **Change a price** | Type the new number in the price box. It saves as soon as you click away. |
| **Hide a sold-out set** | Turn the switch off. The set stays in your dashboard but disappears from the website. Turn it on to bring it back. |
| **Change photos or name** | Click **Edit**. You can add more photos, remove photos, or click **Make main** to choose the photo customers see first. |
| **Change the order** | Use the up and down arrows. The top of the list is the top of the website. |
| **Delete a set** | Click **Delete** and confirm. This can't be undone, so use the hide switch if you're unsure. |
| **Back up** | Click **Download backup** now and then to keep a copy of your product list. |

Photos from your phone are resized and compressed automatically, so you can upload them straight from your gallery.

---

## Option B: no database (local mode)

If `config.json` is left empty, the dashboard runs in **local mode**:

1. Open `your-website.com/admin.html`. There's no password in this mode.
2. Make your changes. They're saved in that browser only.
3. Click **Download products.json**.
4. Upload that file to your hosting, replacing the old `products.json`. The website now shows your changes.

Local mode is fine for small updates. It holds roughly 30 to 40 new photos before the browser runs out of space. You also have to re-upload the file after each change, so switch to Option A when you can.

---

## Where to host

### GitHub Pages

This repository includes a GitHub Actions workflow that publishes the website whenever you push to `main`.

1. In the repository on GitHub, open **Settings** > **Pages**.
2. Under **Build and deployment**, choose **GitHub Actions** as the source.
3. After the first successful deployment, open the Pages URL shown on that settings page.

The site files, including `admin.html`, are publicly accessible to visitors. Leave Supabase keys blank until you configure Supabase, and only use the public anon/publishable key in `config.json`.

Other hosts that serve plain files also work:
- **Netlify Drop** (app.netlify.com/drop): drag the folder onto the page and it's live. To update a file later, drag the folder again.
- **Vercel**
- **cPanel / shared hosting:** upload the folder through File Manager.

With Option A, you only upload the folder once. All later changes happen in the dashboard.
