# Start or Sit

A simple, just-for-fun fantasy football "start or sit" decider.

Type in two player names and tap **Decide**. The app flips between the two names for about a second, then shows:

- **START**: the chosen player
- **BENCH**: the other player
- A random, lighthearted reason for the pick
- A random confidence percentage (51% to 99%)

**Decide again** reruns the pick with the same players. **New matchup** clears both names.

Picks are random. This is not real fantasy advice.

## How it's built

The whole app is one file: `index.html`, with the HTML, CSS, and JavaScript inside it. There is no database, no login, no back end, and no build step.

## Run it locally

1. Download or clone this repository.
2. Double-click `index.html` to open it in your web browser.

## Publish it on Netlify

1. Go to [netlify.com](https://www.netlify.com) and log in (you can sign up with your GitHub account).
2. On your Netlify dashboard, click **Add new project** (it may say **Add new site**), then **Import an existing project**.
3. Choose **GitHub** and give Netlify permission to access your repositories if it asks.
4. Select the **start-sit** repository.
5. On the build settings screen:
   - **Branch to deploy:** `main`
   - **Build command:** leave this blank
   - **Publish directory:** leave this blank (or enter `.`), which means the repo root
6. Click **Deploy**.
7. When the deploy finishes, Netlify shows your site's link (something like `random-name-123.netlify.app`). Click it to open the app.
8. Optional: to change the link name, go to **Project configuration** (or **Site configuration**) > **Change project name**.

Any time you push a change to the `main` branch on GitHub, Netlify will update the site automatically.
