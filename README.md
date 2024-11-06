# freeCodeCamp

freeCodeCamp is an open-source learning platform for studying programming, mathematics, computer science, and developer-focused language skills through interactive lessons, projects, quizzes, exams, and certifications.

This repository contains the production learning application, API, curriculum source, shared packages, developer tools, automated tests, and localization infrastructure used by the platform.

## Overview

freeCodeCamp provides a self-paced learning environment built around hands-on practice. Learners progress through structured certifications, complete required projects, take exams, and maintain a persistent profile containing their progress and earned credentials.

The platform supports:

- Full-stack web development
- JavaScript and frontend development
- Python
- Relational databases
- Backend development and APIs
- Programming interview preparation
- Mathematics and computer science practice
- Developer-focused language learning
- Project-based certification workflows

## Features

### Learning Experience

- Thousands of interactive coding challenges
- Guided lessons, workshops, labs, reviews, and quizzes
- Browser-based code editors
- Interactive previews and challenge test runners
- Required certification projects
- Certification exams
- Persistent learner progress
- Public profiles and completed certifications
- Search across learning content
- Multiple curriculum languages
- Responsive desktop and mobile experience

### Certifications

The current full-stack curriculum includes certification paths for:

- Responsive Web Design
- JavaScript
- Front-End Development Libraries
- Python
- Relational Databases
- Back-End Development and APIs

The platform also contains developer-oriented language certification tracks and additional preparation content for coding interviews, algorithms, mathematics, and programming practice.

### Platform Capabilities

- User authentication and session management
- OAuth-based sign-in support
- Curriculum localization
- Challenge-specific build and validation tooling
- Search integration
- Donation and payment workflows
- Feature flags
- Email delivery
- API documentation
- Error tracking and application telemetry
- Automated curriculum validation
- End-to-end browser testing

## Tech Stack

| Area | Technologies |
| --- | --- |
| Runtime | Node.js 24 or later |
| Package manager | pnpm 10 or later |
| Monorepo tooling | Turborepo |
| Language | TypeScript, JavaScript |
| Frontend | Gatsby 5, React 18 |
| Client state | Redux Toolkit, Redux Saga |
| Code editors | Monaco Editor, Sandpack |
| Styling | PostCSS, Tailwind CSS |
| Localization | i18next |
| Search | Algolia |
| Backend | Fastify 5 |
| API schema | Swagger, TypeBox |
| Data access | Prisma |
| Database | MongoDB |
| Authentication | OAuth 2.0, JWT, cookies |
| Payments | Stripe |
| Email | Nodemailer, Amazon SES-compatible SMTP |
| Observability | Sentry |
| Unit testing | Vitest, Testing Library |
| API testing | Supertest, Mock Service Worker |
| End-to-end testing | Playwright |
| Quality tooling | ESLint, Prettier, Stylelint, TypeScript |
| Local services | Docker Compose |

## Installation

### Requirements

For local development, use:

- Node.js 24.x
- pnpm 10.x
- MongoDB 8.x
- Docker Compose 2.x
- Git
- At least 8 GB of RAM
- Approximately 8–10 GB of free disk space

Linux or macOS is recommended for native development. Windows users should use WSL with Docker Desktop.

### Install Dependencies

From the repository root:

```bash
pnpm install
```

The installation also prepares workspace packages and Git hooks.

### Create the Environment File

```bash
cp sample.env .env
```

The default development values are sufficient for the core local application.

External services such as authentication providers, search, payments, telemetry, and AI-assisted features require their own credentials.

### Start MongoDB

The development database must run as a MongoDB replica set.

Start the provided service:

```bash
docker compose -f docker/docker-compose.yml up -d
```

The default database uses port `27017`.

### Seed Development Data

Create a local development user and required application data:

```bash
pnpm run seed
```

Create a user with completed certifications when testing profile and certification behavior:

```bash
pnpm run seed:certified-user
```

### Start the Platform

```bash
pnpm run develop
```

This starts both the API and learning client.

The default development ports are:

```text
Client: 8000
API:    3000
```

The API documentation interface is also served by the development API.

## Curriculum Development

Building the entire curriculum can be resource intensive. Selective builds are recommended when working on specific learning content.

### Build One Certification Area

```bash
FCC_SUPERBLOCK=responsive-web-design pnpm run develop
```

### Build One Curriculum Block

```bash
FCC_BLOCK=basic-html-and-html5 pnpm run develop
```

### Build One Challenge

```bash
FCC_CHALLENGE_ID=challenge-id pnpm run develop
```

These filters reduce startup and rebuild time while developing individual curriculum areas.

### Audit Curriculum Challenges

```bash
pnpm run audit-challenges
```

### Build Curriculum Data

```bash
pnpm run build:curriculum
```

## Usage

### Learner Workflow

1. Start the application and open the learning client.
2. Sign in with the seeded development user.
3. Select a certification or learning path.
4. Complete lessons, workshops, labs, reviews, and quizzes.
5. Run challenge tests directly in the browser.
6. Complete the required certification projects.
7. Take the certification exam when eligible.
8. Review completed work and progress from the user profile.

### Development User Data

The standard seed command creates a development account with incomplete certifications.

Use:

```bash
pnpm run seed
```

For completed certification scenarios:

```bash
pnpm run seed:certified-user
```

Reseeding may replace existing local user state and require signing in again.

## Configuration

The application reads development settings from `.env`.

### Core Settings

| Variable | Purpose |
| --- | --- |
| `MONGOHQ_URL` | MongoDB connection |
| `FREECODECAMP_NODE_ENV` | Application runtime environment |
| `DEPLOYMENT_ENV` | Deployment category |
| `HOME_LOCATION` | Client application location |
| `API_LOCATION` | API service location |
| `CLIENT_LOCALE` | Client interface language |
| `CURRICULUM_LOCALE` | Curriculum language |
| `SHOW_UPCOMING_CHANGES` | Enables work-in-progress curriculum |

### Authentication and Security

| Variable | Purpose |
| --- | --- |
| `AUTH0_CLIENT_ID` | OAuth client identifier |
| `AUTH0_CLIENT_SECRET` | OAuth client secret |
| `AUTH0_DOMAIN` | Authentication provider domain |
| `SESSION_SECRET` | Session signing secret |
| `COOKIE_SECRET` | Cookie protection secret |
| `JWT_SECRET` | JWT signing secret |

### Search and Payments

| Variable | Purpose |
| --- | --- |
| `ALGOLIA_APP_ID` | Search application identifier |
| `ALGOLIA_API_KEY` | Search API credential |
| `STRIPE_PUBLIC_KEY` | Client payment key |
| `STRIPE_SECRET_KEY` | Server payment credential |
| `PAYPAL_CLIENT_ID` | PayPal integration identifier |
| `PATREON_CLIENT_ID` | Patreon integration identifier |

### Observability

| Variable | Purpose |
| --- | --- |
| `SENTRY_DSN` | Backend error-reporting configuration |
| `SENTRY_CLIENT_DSN` | Client error-reporting configuration |
| `SENTRY_ENVIRONMENT` | Telemetry environment |
| `SENTRY_SERVER_NAME` | API service name |
| `SENTRY_TRACES_SAMPLE_RATE` | Trace sampling rate |

### API Development Flags

| Variable | Purpose |
| --- | --- |
| `FCC_ENABLE_SWAGGER_UI` | Enables API documentation UI |
| `FCC_ENABLE_DEV_LOGIN_MODE` | Enables local development login |
| `FCC_ENABLE_SHADOW_CAPTURE` | Controls shadow request capture |
| `FCC_ENABLE_SENTRY_ROUTES` | Enables Sentry-specific routes |
| `FCC_ENABLE_CLASSROOM` | Enables classroom functionality |
| `FCC_API_LOG_LEVEL` | API log level |
| `FCC_API_LOG_TRANSPORT` | API log output format |
| `FCC_DRAIN_TIMEOUT_MS` | Graceful API shutdown timeout |

### Email

| Variable | Purpose |
| --- | --- |
| `EMAIL_PROVIDER` | Selects the email delivery implementation |
| `SES_SMTP_USERNAME` | Production SMTP username |
| `SES_SMTP_PASSWORD` | Production SMTP password |
| `SES_SMTP_HOST` | Production SMTP host |

Keep all production credentials outside version control.

## Available Scripts

Install dependencies:

```bash
pnpm install
```

Start full development mode:

```bash
pnpm run develop
```

Build all workspaces:

```bash
pnpm run build
```

Build only the client:

```bash
pnpm run build:client
```

Build only the API:

```bash
pnpm run build:api
```

Run all tests:

```bash
pnpm run test
```

Run client tests:

```bash
pnpm run test-client
```

Run API tests:

```bash
pnpm run test-api
```

Run curriculum content tests:

```bash
pnpm run test-curriculum-content
```

Run end-to-end tests:

```bash
pnpm run playwright:run
```

Run type checks and linting:

```bash
pnpm run lint
```

Format supported files:

```bash
pnpm run format
```

Clean generated data and dependencies:

```bash
pnpm run clean
```

## Testing

### Unit and Integration Tests

The client and API use Vitest-based test suites.

Run the complete test workflow:

```bash
pnpm run test
```

### End-to-End Tests

Install browser and system dependencies when required:

```bash
pnpm run playwright:install-build-tools
```

Run browser tests:

```bash
pnpm run playwright:run
```

### Curriculum Validation

Curriculum changes should be validated separately:

```bash
pnpm run test-curriculum-content
pnpm run audit-challenges
```

## Contributing

freeCodeCamp is developed by a large open-source contributor community. Contributions can include curriculum improvements, bug fixes, tests, translations, developer tooling, documentation, and platform features.

Before submitting changes:

- Create a focused branch
- Sync with the current upstream branch
- Keep changes limited to a clear issue or improvement
- Add or update tests for behavioral changes
- Validate curriculum changes with the relevant curriculum tools
- Run TypeScript and lint checks
- Run affected unit tests
- Run Playwright tests for user-facing workflows when appropriate
- Preserve localization support for visible text
- Avoid committing `.env` files or credentials
- Keep generated curriculum data synchronized when required
- Follow the repository's established contribution and code-of-conduct requirements
