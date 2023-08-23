![DuckPass](/img/ducky.png)

# Project description

With the surge in cybersecurity incidents, the need to safeguard our data has become more pressing than ever. 
In 2022, Sortlist's statistics revealed a staggering exposure of 22 billion records due to over 4,100 data breaches. 
In the face of this landscape, digital security has taken center stage, both for businesses and individuals, who are keen on preserving the integrity of their information.

Current reality shows that 95% of hacking incidents stem from human errors and inadequate cybersecurity practices. 
Among prevailing bad habits, the use of predictable and easily discoverable credentials poses a significant threat. 
The complexity of remembering multiple strong passwords often leads to the adoption of easily memorable identifiers, subsequently resulting in their reuse.

The DuckPass project comes to life as an innovative password manager. 
Its aim? To aggregate and secure these intricate passwords, all while offering a seamless and reassuring experience. 
In addition to introducing a single master password requirement for easy access to the platform without compromising security, DuckPass sets itself apart by providing a groundbreaking feature. 
Users can now determine if their credentials have been compromised in previous data breaches, further enhancing their digital security. 
Armed with features like generating highly secure passwords, DuckPass is a robust solution fortified by end-to-end encryption, ensuring your data's security for complete peace of mind.

# Functional requirements

- Sign in
- Sign up
- Login
- Password forgotten
- 2FA login
- Search logins
- Add username/password securely in the vault
- Remove logins from the vault
- Vault timeout: after n minutes of inactivity the vault become blocked and encrypted
- Generate secure password
- Store notes securely
- (FIDO2?)

# Non-functional requirements

- End-to-end encryption
- Zero-knowledge encryption


# Technologies

Frontend app:
- React + TypeScript
- Tailwind CSS

Backend app:
- FastAPI + uvicorn (python)
- Gunicorn (Python web server WSGI)

CI/CD:
- Docker
- GitHub Actions
- TypeScript testing framework: Jest
- Python testing framework: pytest
- Hosting on Heroku for the backend
- Hosting on Netlify for the frontend

Domain :
- Cloudflare

# Architecture 

![App's architecture](img/architecture.png)

The client side is a web server hosted on Netlify. We have two environments on Netlify, one for pre-production (duckpass.ch) and the production one (duckpass.ch).

It's an application built using React and TypeScript, primarily allowing the user to access their data, and also enabling us to secure the data before it's sent to the server.

The user's encrypted information is sent to the API (hosted on Heroku) through a secure channel. The endpoint that retrieves the data will send it to another part of the Python code, which then stores it in the PostgreSQL database.

# Project Management

- Scrum
    - Sprint (1 week) planning each week on monday
    - Daily Scrum, 10-15'
    - Product Backlog
    - Sprint Backlog
    - Definition of Done (DoD)

Each sprint will cover 1 week with a daily scrum of 10-15 minutes long on each morning to plan our daily tasks. We'll also organized a little retrospective each evening to gather our difficulties of the day.

The Product Owner will review and accept each features before passing them from the "In review" to the "Deployed" column.

## Kanban organization

The scrum-related kanban will be implemented with GitHub Project linked to the organization DuckPass.

Here is a little summary of each column:

    - Product backlog: tasks to be done by the end of the project's deadline
    - Sprint backlog: tasks to be done by the sprint
    - In progress: tasks currently being done
    - Testing: tasks potentially finished but still need to be test
    - In review: tasks that need to be accepted by the Product Owner
    - Ready : tasks totally finished on the pre-prod env and accepted but need to be deployed on prod
    - Deployed: tasks deployed, accepted and tested on production

![Kanban workflow graph](img/tasks.png)

### Tasks priority
- High : Must be done today
- Medium : Must be done this week
- Low : No due date

### Tasks size
- Large (> 5h)
- Medium (2h < 5h)
- Small (1h < 2h)
- Tiny (< 1h)

## Branch naming convention

Code Flow Branches:
- `main`: prod
- `staging`: preprod (ready)
- `dev`: development

Temporary Branches:
- `feature/xxx`: any code change, must be related to an issue

Here is a little summary how to deal with them :

![Branch dev diagram](./img/branch-dev-diagram.png)

## Commit convention

We'll follow the [Angular Commit Convention](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines) for commit messages:

The format will be the following:
```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

Each line must be less than 100 characters.

The footer should contain a closing reference to an issue if any.

The types we'll likely use are:
- chore (internal changes not related to the end-user)
- style
- feat
- refactor
- test
- fix
- docs

Here is an example:
```
feat(auth): Added user login page feature

Bla bla bla

Closed issue #10000
```

# CI/CD

DuckPass is built with two different environments : production and staging.

The staging environment is only used by the Product Owner to review the final result of the modifications. If the modifications are accepted the code is pushed onto the `main` branch (prod).

Here is a little diagram of the CI/CD pipeline :

![CI-CD Diagram](./img/ci-cd-diagram.png)

The CI workflow is powered by GitHub Actions available on each repository which will in fact just run a `npm run test`.

The continuous deployment is managed by Netlify and Heroku portals directly linked to the repositories.

# Team member

- ANNEN Rayane: Product owner, frontend developer
- DUCOMMUN Hugo: Scrum Master, frontend developer
- MARTINS Alexis, Backend developer
- SAEZ Pablo, Backend developer