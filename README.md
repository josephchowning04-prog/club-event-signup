# Fall Sky Weekend Signup

A small signup page for a fictional club (Harbor Lights Astronomy Club). A visitor types a name, picks one of three sessions, and gets a confirmation. Signups are saved, and you can search them by name. All names and data are made up.

## How the pieces fit together (plain English)

- **The browser** is the page you see and click. It shows the form, checks that you typed a name and picked a session, and shows the confirmation or error messages.
- **The server** is a small program running on your computer (`server.js`). The browser sends it the signup. The server double-checks it, saves it, and sends back the confirmation wording.
- **The saved signups** live in a database. On your computer that is one file called `signups.db`, created automatically the first time you run the app. When the app is online, they can live in a hosted database instead (see the last section).

Browser -> server -> database, and back again. Searching works the same way.

## What you need

- **Node.js**, version 22.5 or newer (free, from nodejs.org). To check, open a terminal and type `node --version`.
- Nothing else for the local version. (`npm install` is only needed for hosting; it is safe to run either way.)

## Setup and start commands

1. Open a terminal in this folder (the one with `server.js` in it).
2. Install: `npm install`
3. Start the app:

   ```
   npm start
   ```

   (If `npm` is not found, `node server.js` does the same thing.)
4. You should see "Signup app running at http://localhost:3000". Open that address in your browser.
5. To stop the app, click the terminal and press Ctrl+C.

You may see a line saying SQLite is "experimental". That is normal and harmless.

## Try it

- **Sign up:** type `Maya Chen`, choose "Constellation Walk", press Sign Up. You should see: `You're signed up, Maya Chen! Session: Constellation Walk (Sat 8:00 PM).`
- **Check the errors:** leave the name blank (or type only spaces) and press Sign Up. You should see "Please enter your name." and your chosen session stays selected.
- **Search:** under "Find a signup", type `Maya` and press Search.
- **Automatic check:** with the app running, open a second terminal in this folder and run `npm test`. It runs the three examples from `design.md` plus a search.

## Use a hosted database (optional)

Without any setup, the app uses the local file. To use a hosted PostgreSQL database instead:

1. Run `npm install` (this installs `pg`, the hosted-database package).
2. Copy `.env.example` to a new file named `.env`.
3. In `.env`, remove the `#` in front of `DATABASE_URL` and replace the placeholder words (`YOUR_USER`, `YOUR_PASSWORD`, `YOUR_HOST`, `YOUR_DATABASE`) with the values your database provider gives you.
4. Run `npm start`. The first line it prints will say it is saving to the hosted database.

To go back to local, put the `#` back in front of `DATABASE_URL` (or delete `.env`).

### Settings the app reads (names only)

- `DATABASE_URL` - the hosted database address. If it is missing, the local file is used.
- `DATABASE_SSL` - set to `true` if your database provider requires it.
- `PORT` - the port to listen on. Hosts like Render set this for you; the default is 3000.

### Putting it on a host such as Render

- Build command: `npm install`
- Start command: `npm start`
- Environment variables: add `DATABASE_URL` (and `DATABASE_SSL` if needed) in the host's settings page, not in the code.
- If `DATABASE_URL` is not set on the host, the app falls back to the local file. On a free host that file can disappear when the service restarts, so use the hosted database to keep signups.

**Never put a real password in a file you share or upload.** `.env` is listed in `.gitignore` so it is not uploaded by accident. `.env.example` contains placeholders only.

## Files

- `server.js` - the server and database code
- `public/index.html` - the page (layout, labels, and messages from `design.md`)
- `test.js` - the automatic check
- `.env.example` - placeholder settings for the hosted database
