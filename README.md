# Start or Sit

A fantasy football start/sit decider for **PPR** leagues. Type in two players and it tells you which one to start this week, based on:

- **This week's projection** (PPR points)
- **Recent form** (average PPR points over the player's last 3 games)
- **Matchup** (how many PPR points the opponent's defense allows per game to that position, ranked against the rest of the league)
- **Injury and bye status**

It shows START and BENCH, a plain-English reason, a confidence level, and a side-by-side table of the numbers so you can check the call yourself.

Recommendations are estimates, not guarantees. No app knows who will actually score more.

## How it's built

The whole app is one file: `index.html`, with the HTML, CSS, and JavaScript inside it. There is no database, no login, no back end, and no build step.

### Where the data comes from

When the page opens, your browser pulls live data straight from the free [Sleeper](https://sleeper.com) public API:

1. The current NFL season and week.
2. This week's PPR projections for every QB, RB, WR, TE, K, and team defense.
3. Actual stats from every earlier week this season. These are used to find each player's last 3 games and to work out how many PPR points each defense gives up to each position.

The projection and stats endpoints are not officially documented by Sleeper, so they could change without notice. If the live data doesn't load for any reason, the app switches to **manual entry** (see below).

### How the pick is made

1. **Base score** = 60% of this week's projection + 40% of the average of the last 3 games. If a player has no recent games, the base score is just the projection.
2. **Matchup adjustment:** the opponent's defense is ranked against the position (1 = allows the fewest points, toughest; 32 = allows the most, easiest). The toughest matchup lowers the score by up to 8%. The easiest raises it by up to 8%. The adjustment is small on purpose, because projections already account for the matchup somewhat.
3. **Status:** a player who is Out, on IR, suspended, or on bye scores 0. A Doubtful player keeps 30% of their score. Questionable players are flagged but not penalized.
4. The higher score is the START.

**Confidence** is based on the gap between the two scores: under 8% is "Low - close call", 8% to 20% is "Medium", over 20% is "High".

### Manual entry

Click **Enter stats manually instead** (or wait for it to appear automatically if live data fails). For each player, enter:

- Projected PPR points (required)
- Average PPR points over the last 3 games (optional)
- Opponent's rank against the position, 1 to 32 (optional). **1 = toughest defense, 32 = easiest.** Some sites rank it the other way, so check before you type it in.
- Status (Healthy, Questionable, Doubtful, Out, Bye)

You can find these numbers in ESPN, Sleeper, or Yahoo. The app scores them the same way as live data.

## Run it locally

1. Download or clone this repository.
2. Double-click `index.html` to open it in your web browser. You need an internet connection for live data.

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
