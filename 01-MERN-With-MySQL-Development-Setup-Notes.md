# Apical Codes Website --- Development Setup Notes

**Purpose:** Future reference for the initial local development setup of
the Apical Codes website.

**Project domain:** `apicalcodes.com`\
**Local project folder:** `E:/Projects/Apical Codes/apicalcodes`\
**Development environment:** Windows + Visual Studio Code\
**Planned stack:** MySQL, Express.js, React.js, Node.js\
**Hosting plan:** Git/GitHub → Hostinger VPS with CloudPanel →
Cloudflare-managed domain

------------------------------------------------------------------------

## 1. Project Goal

Build the Apical Codes website locally on the laptop, track changes with
Git, push the project to a GitHub repository, and deploy it to the
Hostinger VPS.

The intended application stack is:

-   **React.js:** Frontend user interface
-   **Vite:** Frontend development server and production build tool
-   **Node.js:** JavaScript runtime for development tools and the
    backend
-   **Express.js:** Backend server and API
-   **MySQL:** Persistent application data
-   **Git/GitHub:** Version control and remote source-code repository
-   **CloudPanel / Hostinger VPS:** Production hosting
-   **Cloudflare:** DNS management and optional proxy/CDN

------------------------------------------------------------------------

## 2. What Has Been Completed

### 2.1 Local project folder

The project folder was opened in VS Code:

``` text
E:/Projects/Apical Codes/apicalcodes
```

The following folders were created:

``` text
apicalcodes/
├── client/
└── server/
```

Their intended responsibilities:

-   `client/` --- React frontend application
-   `server/` --- Express backend application

At the time of initial inspection, both folders were empty.

### 2.2 Development tools verified

The following commands were run successfully in the VS Code Git Bash
terminal:

``` bash
node -v
# v22.13.1

npm -v
# 11.1.0

git --version
# git version 2.52.0.windows.1
```

This confirms Node.js, npm, and Git are available in the terminal.

### 2.3 React frontend scaffold created

The following command was run from the project root:

``` bash
npm create vite@latest client -- --template react
```

The Vite project generator was used because it creates a ready-to-use
React project structure and configuration.

During setup:

-   **React template** was selected.
-   **Oxlint** was selected as the linter.
-   **Install with npm and start now? --- Yes** was selected.

The React starter application was then opened successfully in the
browser at:

``` text
http://localhost:5173
```

The displayed page was the default Vite + React starter page.

### 2.4 What this confirms

**Yes --- the frontend has been scaffolded and successfully run
locally.**

However, the actual Apical Codes homepage design and content have not
been developed yet. The current page is only the default starter screen.

------------------------------------------------------------------------

## 3. Why These Choices Were Made

### React

React is used to build the website's interface from reusable components.
Examples include the navigation bar, hero section, service cards,
portfolio items, forms, and footer.

### Vite

Vite provides a fast local development server and prepares optimized
frontend files for production. It also supports Hot Module Replacement
(HMR), allowing many code changes to appear in the browser without a
full reload.

### Oxlint

Oxlint is a JavaScript/TypeScript linter. It helps identify certain
code-quality issues and suspicious patterns. It was selected as a
reasonable, fast option offered by the Vite project generator. ESLint is
also a valid alternative; selecting Oxlint does not mean ESLint is
unsuitable.

### npm

npm installs and manages JavaScript packages. Project dependencies are
recorded in `package.json`, and installed package files are placed in
`node_modules/`.

### Node.js

Node.js allows JavaScript to run outside the browser. It will be used to
run the Express backend and development/build tools.

### Git

Git tracks changes to the project over time. GitHub will host the remote
repository, making it possible to push code from the laptop and later
retrieve it on the VPS.

------------------------------------------------------------------------

## 4. Current Project Architecture

The intended structure is:

``` text
apicalcodes/
├── client/                 # React + Vite frontend
│   ├── public/
│   ├── src/
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   └── ...
│   ├── package.json
│   └── vite.config.js
│
├── server/                 # Express backend (planned)
│
├── .gitignore              # To be reviewed/created
└── README.md               # Project documentation (planned)
```

The exact generated files may vary depending on the Vite version and
selected options.

### How the application will communicate

``` text
Visitor's browser
       |
       v
React frontend (client)
       |
       | HTTP request to an API
       v
Express backend (server)
       |
       | Database query
       v
MySQL database
```

The browser should communicate with MySQL **through the Express
backend**, not directly. Database credentials must never be placed in
frontend code.

------------------------------------------------------------------------

## 5. XAMPP and MySQL --- Current Status

XAMPP is installed on the laptop, according to the user.

At the time this note was prepared, the following actions had been
recommended but were **not yet confirmed as completed**:

1.  Start the MySQL service in XAMPP Control Panel.
2.  Open `http://localhost/phpmyadmin`.
3.  Create a database named `apicalcodes_db`.
4.  Create the Express backend.
5.  Install backend packages:

``` bash
cd server
npm init -y
npm install express mysql2 cors dotenv
```

Do not assume the database or backend packages already exist until their
completion is verified.

**Note:** XAMPP commonly bundles MariaDB, which is MySQL-compatible for
many application use cases. Confirm the database server/version if a
specific Oracle MySQL version is required.

Apache is not required merely to run the React development server or an
Express API. It may be useful for other local XAMPP tools, but it is not
part of the planned application runtime.

------------------------------------------------------------------------

## 6. Local Development vs. Production

  -----------------------------------------------------------------------
  Environment                         Purpose
  ----------------------------------- -----------------------------------
  Laptop                              Develop and test the application

  Local Vite server                   Preview React frontend, currently
                                      on port `5173`

  Local Express server                Run backend API, planned for port
                                      `3000`

  Local XAMPP database                Development database, planned

  GitHub                              Remote source-code repository

  Hostinger VPS                       Production application hosting

  CloudPanel                          VPS site and application management

  Cloudflare                          DNS management; proxy can be
                                      enabled after origin/SSL checks
  -----------------------------------------------------------------------

The local database and production database will be separate. Production
credentials must be stored securely on the VPS and must not be committed
to Git.

------------------------------------------------------------------------

## 7. Important Commands Learned So Far

Run these from the project root unless otherwise specified.

### Check installed tools

``` bash
node -v
npm -v
git --version
```

### Inspect the client folder

``` bash
ls -la client
```

### Create the React + Vite scaffold

``` bash
npm create vite@latest client -- --template react
```

### Start the frontend development server

The Vite setup selected "Install with npm and start now." If the server
is not currently running, use:

``` bash
cd client
npm run dev
```

Then open the local URL printed in the terminal, usually:

``` text
http://localhost:5173
```

To stop a running development server, focus its terminal and press
`Ctrl + C`.

------------------------------------------------------------------------

## 8. Security and Git Safety

Before pushing code to GitHub:

-   Do not commit passwords, API keys, or database credentials.
-   Keep local secrets in environment files such as `.env`.
-   Ensure `.env` files are ignored by Git.
-   A safe example file such as `.env.example` may contain placeholder
    values only.
-   Do not expose MySQL directly to the public internet.
-   Use HTTPS for the production domain.

------------------------------------------------------------------------

## 9. Phase Boundary

### Phase 1 --- Local environment and frontend scaffold

**Status: Completed**

-   [x] Project folder created and opened in VS Code
-   [x] `client/` and `server/` folders created
-   [x] Node.js, npm, and Git verified
-   [x] React + Vite starter project generated
-   [x] Oxlint selected
-   [x] npm setup and development server option selected
-   [x] Default React starter page opened at `localhost:5173`

### Not yet confirmed / future phases

-   [ ] XAMPP MySQL service started
-   [ ] `apicalcodes_db` database created
-   [ ] Express backend initialized
-   [ ] Backend packages installed
-   [ ] React frontend customized into the Apical Codes website
-   [ ] Frontend connected to Express API
-   [ ] Express connected to MySQL
-   [ ] Git repository initialized and pushed to GitHub
-   [ ] VPS deployment configured from GitHub
-   [ ] Production environment variables and database configured
-   [ ] Domain and HTTPS verified end-to-end

------------------------------------------------------------------------

## 10. Resume Point

**Resume from:** Phase 2 --- Backend and local database setup.

Before proceeding, verify whether the XAMPP MySQL service is running and
whether `apicalcodes_db` has been created. Then initialize the Express
application in `server/`, build a simple test API, and connect it to the
local database.

The current frontend milestone is complete: the React + Vite starter
application runs locally.
