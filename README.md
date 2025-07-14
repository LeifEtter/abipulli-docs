# Project Discussion

This document is an in-depth discussion of the AbiPulli Application, where I go over what I have implemented and the reasoning behind my decisions. To give this document structure, I have categorized this discussion into different steps.

### Table of Contents

1. [What is AbiPulli.com? (Quick Refresher)](craftdocs://open?blockId=93DA59F7-CA46-42DA-B425-A013AC908FE9&spaceId=b0e62220-21e7-3e79-e368-d4886dca007e)
2. [Defining Requirements](craftdocs://open?blockId=D4F17C7D-F634-484F-B814-631766DB830C&spaceId=b0e62220-21e7-3e79-e368-d4886dca007e)
3. [Technical Overview](craftdocs://open?blockId=F401091E-773F-49F6-9709-36AFD5B32B35&spaceId=b0e62220-21e7-3e79-e368-d4886dca007e)
4. [Reasoning of Architectural Choices](craftdocs://open?blockId=E4F89383-20E3-430D-A63B-BDCEF050B0FF&spaceId=b0e62220-21e7-3e79-e368-d4886dca007e)
5. [Unified Typing](craftdocs://open?blockId=A7CC0F5D-F2A3-4238-A888-70D79DB16B22&spaceId=b0e62220-21e7-3e79-e368-d4886dca007e)
6. [Code Architecture](craftdocs://open?blockId=7BE3D71E-D23D-4C51-AFF8-CBF81C2AFCC1&spaceId=b0e62220-21e7-3e79-e368-d4886dca007e)
7. [Routing](craftdocs://open?blockId=8733D0D3-90A8-45D9-85EB-DCE9F5F9CE59&spaceId=b0e62220-21e7-3e79-e368-d4886dca007e)
8. [State Management (Frontend)](craftdocs://open?blockId=7B6D57C8-F621-4ADA-910F-A1AD5C955DDD&spaceId=b0e62220-21e7-3e79-e368-d4886dca007e)
9. [Testing](craftdocs://open?blockId=9B4FEA32-563E-4641-9A42-A60D19E89237&spaceId=b0e62220-21e7-3e79-e368-d4886dca007e)
10. [Documentation](craftdocs://open?blockId=E6E5B812-CBCC-4E63-B7F9-623560C77041&spaceId=b0e62220-21e7-3e79-e368-d4886dca007e)
11. [Logging](craftdocs://open?blockId=C8BD538F-0756-492D-BF33-73EDCA4AB58E&spaceId=b0e62220-21e7-3e79-e368-d4886dca007e)
12. [Hosting](craftdocs://open?blockId=8E73E063-9599-474B-9A44-DFA855366E66&spaceId=b0e62220-21e7-3e79-e368-d4886dca007e)
13. [CI/CD](craftdocs://open?blockId=E6F15EF4-A68D-42B9-82AF-BF63F80FEBD6&spaceId=b0e62220-21e7-3e79-e368-d4886dca007e)
14. [Security](craftdocs://open?blockId=0960DE24-6E92-44EA-A19B-46AD2C300AA0&spaceId=b0e62220-21e7-3e79-e368-d4886dca007e)
15. [Accessibility/SEO](craftdocs://open?blockId=C0D84FA1-BEA2-430B-8738-3371A63F170A&spaceId=b0e62220-21e7-3e79-e368-d4886dca007e)

---

1. What is AbiPulli.com? (Quick Refresher)

The AbiPulli project was originally an attempt to digitize the business "[https://abipulli.com](https://abipulli.com)", which mainly operated through analog communication. [Abipulli.com](Abipulli.com) provided design services for soon-to-graduate students wanting to design a Pullover for individual students or the entire grade of a school to celebrate their graduation. Users would contact the team, which would then work with a designer to iterate and finally deliver a batch of pullovers.

---

2. Defining Requirements

During our research on how best to stand out to competitors with a digital product, we distilled through interviews what our users need and their pain points. The students we interviewed were either still thinking about creating Abipullis, currently doing so, or had already ordered them previously:

![Image.png](https://resv2.craft.do/user/full/b0e62220-21e7-3e79-e368-d4886dca007e/doc/577C9F7A-056A-4AAE-AD89-A609725DF83A/5BBEDE48-ED9E-4E1F-997B-72F4EE7B06CA_2/CHnQzItLxJK4aFwDW0j9Lj73kGtAayjiHgvY5yLrMPYz/Image.png)

I turned these interviews into User Stories to better visualize the requirements we will need to fulfill:

![Image.png](https://resv2.craft.do/user/full/b0e62220-21e7-3e79-e368-d4886dca007e/doc/577C9F7A-056A-4AAE-AD89-A609725DF83A/4E6EBF0C-063B-4867-A02D-715A89610282_2/ipUYhPKlMwjJVykk9aDgx0v8h0Rxm4gMr0MmD5nmdfYz/Image.png)

Typically, users have two options when designing Abipullovers:

1. Use a service (such as akhoodies/shirtival) and pick from pre-designed pullovers
2. Work together with a designer (previously abipulli.com/abchlusspullis.de)

During our interviews, we noticed a pattern. Almost all of the students wanted individual designs and only considered opting for services with predesigned pullovers if the budget was too tight or if they ran out of time. Standing out among competitors would mean filling a niche, where students can have the positives of individualized designs without the downsides of lengthy back-and-forth with a designer, or high costs.

Our idea was to use generative AI, which we found out is pretty good in generating text by now, to help students bring their designs to life.

Brainstorming what else our application could need and utilizing the user stories, we created a story map, where we collected all the pages and subpages we would need and their contents. This is an early version of our concept, as afterwards we kept refining our requirements through design specs.

As the image is too large to show at once, I split it up into a left and right side.

![Screenshot 2025-07-14 at 16.07.53.png](https://resv2.craft.do/user/full/b0e62220-21e7-3e79-e368-d4886dca007e/doc/577C9F7A-056A-4AAE-AD89-A609725DF83A/1EB33C1C-452B-47A6-BFC6-63C69C7A072D_2/8XJVvk2rtRolmi6gVou37lakFRyYagCHDLTLhdyxx5sz/Screenshot%202025-07-14%20at%2016.07.53.png)

![Screenshot 2025-07-14 at 16.07.58.png](https://resv2.craft.do/user/full/b0e62220-21e7-3e79-e368-d4886dca007e/doc/577C9F7A-056A-4AAE-AD89-A609725DF83A/D8E49542-736D-4A61-9811-4B227A4C13A1_2/v76DmguNCy8NdkxCxtfBubuk25XeU2i30JkqrQd8Ij8z/Screenshot%202025-07-14%20at%2016.07.58.png)

Later on, I gathered all requirements in a flowchart. This flowchart is a representation of the path a user takes through the app:

![Image.png](https://resv2.craft.do/user/full/b0e62220-21e7-3e79-e368-d4886dca007e/doc/577C9F7A-056A-4AAE-AD89-A609725DF83A/9AE6D2F8-935F-46EA-A56E-7D629A5A4372_2/3m7ioy6XPiCuVR8dk0qdHpCHPlURElZ1Acxwz0xA55Az/Image.png)

I also made more specific design specs for each page:

![Image.png](https://resv2.craft.do/user/full/b0e62220-21e7-3e79-e368-d4886dca007e/doc/577C9F7A-056A-4AAE-AD89-A609725DF83A/13029918-38AE-44B7-AF5E-9597167CB51F_2/9MmO08wKKcs6eAqKTFNwxtnQmGwWNJedAACPwRxB0KYz/Image.png)

These were updated every couple of weeks to reflect changes in requirements. The current Webapp does not fully reflect the flowchart, is i skimmed down the requirements for the hand-in.

---

3. Technical Overview

The Project consists of four main components of code:

| Name                 | Lang. | Frameworks      | Noteworth Libraries    |
| -------------------- | ----- | --------------- | ---------------------- |
| abipulli-frontend    | TS    | React, Tailwind | Tanstack Router, Konva |
| abipulli-backend     | TS    | Express         | Drizzle                |
| abipulli-types (NPM) | TS    |                 | Zod                    |

Additional information about the tech stack can be found in the READMEs:

[abipulli-frontend/readme](https://github.com/LeifEtter/abipulli-frontend/README.md), [abipulli-backend/](https://github.com/LeifEtter/abipulli-frontend/README.md)[readme](https://github.com/LeifEtter/abipulli-backend/README.md),

Additionally, the project uses a PostgreSQL database and Hetzner's Object Storage service for storage. The entire stack is hosted on a Hetzner VPS and connected to my domain through a Cloudflare Proxy.

---

4. Reasoning of Architectural Choices

**Frontend**

For the Frontend, I went with React due to its popularity and my previous experience using it. I chose it over vanilla js due to the dynamic nature of the Application.
I had used NextJS before and was considering it for the project, mainly to generate static pages and improve SEO and performance. Yet I decided to go with React as we will have a Landing Page as the main point of access to the Web App, and this will be done in something like WordPress.
Typescript is, of course, my first choice for applications, as it helps catch errors during coding.
Tailwind was my go to for styling. It allows me to style components inline, forgoing the need for style sheets and enabling fast styling of components.

**Backend**

ExpressJS was my choice for the backend due to previous experience using it and the fact that I want to unify types between the applications.
Previously, I had used pure SQL and Prisma for projects. Pure SQL was too complex to maintain, and Prisma didn't feel integrated enough into TypeScript, so I went with Drizzle as my ORM. Drizzle lets me infer types from schemas and directly use these in my code. While I am aware that, as a newer library, Drizzle is less stable and has a much smaller community, the benefits outweigh these downsides for me.

**PostgreSQL**

I don't really have a preference between MySQL and PostgreSQL, but I went with SQL over NoSQL due to my preference for strict schema enforcement and consistency. Due to the nature of the application being used by mainly a single student representing a lot of other students, we don't expect to have high traffic, so I don't see much use that NoSQL provides with the ease of horizontal scalability.

---

5. Unified Typing

As both my Frontend and Backend were developed with TypeScript, I decided to have a unified typing system. This would give me the following benefits:

- Using types like Image/User/Pullover in both the Frontend and Backend simplifies data conversion
- Easier Error Handling through Shared Error Libraries
- Universal Schemas for typing and validating requests and responses

The last reason was a big pain point in previous projects, where I didn't have a way to check if my request bodies were correct before actually running the requests against the backend.

To implement unified typing, I went with a package called Zod. Zod let me create schemas that I could also use to validate requests at runtime on the backend, and then I inferred TypeScript types from the schemas, for compile-time validation. I was thinking long about how to approach this to avoid confusion between Zod Schemas and Types, and decided that almost all of my types would be inferred from Zod Schemas.

This would make Zod schemas the source of truth.

To make the types accessible across the frontend and backend, I created an npm package "abipulli-types". At first, I was abusing npm version patch and npm publish to make simple changes to types and release them (that's why the version number is so high), but soon found out about npm link, which helped me propagate changes locally quickly, without the need for publishing the package every time.

A downside of this way of development was the need to maintain an extra npm package and adapt both the frontend and backend when making changes to the types of packages. This makes versioning a lot harder.

---

6. Code Architecture

**Backend**

I used a Layer-First approach with Routers, Controllers, Services, etc., to separate and organize my code. My reason for going with Layer-First in comparison to Feature-First is that it is easier to maintain and to keep everything consistent. Suppose I wanted to move logic from one feature to another (as often happens in quickly growing projects). In that case, it's much easier to go with this approach as it means not having to extract the logic completely from a feature but instead just move it over within the layer.
The following table gives an overview of the simplified layer structure

| Layer/Folder | Purpose                                                                                         |
| ------------ | ----------------------------------------------------------------------------------------------- |
| /routes      | Handles all incoming requests, authenticates, validates and calls the corresponding controllers |
| /middleware  | Take care of validation, authentication, authorization, errorHandling, file management          |
| /controllers | Call services to get/delete/manipulate data and return a corresponding response                 |
| /services    | Contain Business Logic, communicate with database to get/delete/manipulate data                 |
| /db          | Contains the (Drizzle) Database Schemas                                                         |

Maintaining these layers helps me isolate processes from each other, allowing easier testing and refactoring.

**Frontend**

The frontend is a mix of a Layer- and Feature-First approach. While pages inside the routes folder are grouped by feature, all pages are in a single folder, and in the components folder, a mix of feature-based separation and use-case separation is used.
Due to the nature of file-based routing in Tanstack Router, it is hard to commit to a fully feature-first approach. The files themselves and their location in the directory decide the URL paths.
The following table gives an overview of the frontends layer architecture:

| Layer/Folder | Purpose                                                                                         |
| ------------ | ----------------------------------------------------------------------------------------------- |
| /api         | Contains all logic necessary for handling api calls                                             |
| /assets      | Contain images/icons                                                                            |
| /components  | React Components used in the pages                                                              |
| /routes      | Pages managed by Tanstack Router                                                                |
| /providers   | Context and Provider for each State                                                             |
| /hooks       | Custom Hooks, mainly for providing easy access to methods and values contained inside providers |
| /utilities   | Independant utility functions                                                                   |
| /types       | Frontend specific Types                                                                         |

---

7. Routing

My previous projects were implemented using either a Single-Page approach or NextJS.

I wanted to take this project down a router-based approach for the following reasons:

- Better separation between views
- Benefits of having a real URL (user experience and also sharing a specific page, which might be important for users collaborating in creating a pullover)
- Later, SEO implementation will be much easier

As mentioned before, I went with Tanstack Router for routing. Tanstack Router provides me with a couple of pros over React Router. For one, it enables type safety of params and search queries and supports route guards. While I don't take enough advantage of these pros right now, I will make use of them as the project grows.

---

8. State Management (Frontend)

In the Application, some flows collect information across multiple screens (ex., Onboarding, Image Generation). To manage data across the different pages and allow easy retrieval and saving to localStorage, I created a combination of Context, Provider, and CustomHook. I also applied this pattern to other things, such as the Snackbar, Accept Decline Popup, and Auth Management.
This also lets me extract business logic out of the pages. The Providers manage the page's value and error states, and make calls to the backend. With a separated business logic, I also have an easier time testing the business logic, as I don't have to render an entire screen.

---

9. Testing

Both the frontend and backend have partial test suites.
The frontend test file has factories for generating data and mocks for API designs. While it does have Integration tests, namely testing the custom hooks and their states, the general test suite needs improvement.
The backend mostly has end-to-end/integration tests for the routes, and uses testcontainers to simulate a database to avoid pollution during testing.

---

10. Documentation

Besides the README.md files the Projects uses TSDoc to explain some functions. See /api in frontend.

---

11. Logging

The backend uses Pino for logging to console. It logs through functions like logger.error, but also logs every api request and request/response data, using pino-http.

---

12. Hosting

When I was choosing the best way to host my application, two services came to mind at first:

AWS and DigitalOcean. As I had used both of these already before, I thought i would go with one of those. Yet I had a lot of running costs for the last project, where I had gone with AWS (specifically RDS and EC2). The monthly bills would end up at about 40€-50€. When evaluating if DigitalOcean was the right approach, I realized I could host on a VPS instead, due to the following advantages:

- Full Control of the environment
- No Vendor Lock-In. Can always migrate to another service
- Lower running costs (3-4€ compared to at least 30€ at AWS)
- Risk mitigation. Costs can't get higher than the VPS rental costs

I weighed this against the cons, which are primarily:

- Single Location for VPS → Low speed for international users
- More complicated Horizontal Scaling
- Higher Responsibility in terms of security (Permissions, DDOS, etc..)

Despite the cons, I decided to go with Hetzner. As most users come from the German region, the Hetzner location of Nürnburg wouldn't be a problem. Scaling would be harder, but a class/grade representative normally buys Abschlusspullover for the entire grade. This means one customer orders products for 50-100 other customers, which means lower traffic. As I already wanted to go with the VPS approach as a learning opportunity, this seemed like the right pick.

For the domain hosting, I went with Cloudflare, as it is the largest provider of CDNs globally, so everything would integrate seamlessly in terms of caching.

This Graph gives an overview of how the application is hosted:

![Image.png](https://resv2.craft.do/user/full/b0e62220-21e7-3e79-e368-d4886dca007e/doc/577C9F7A-056A-4AAE-AD89-A609725DF83A/92f2238c-0f77-36c4-97bc-e3fef8901f4b/MB7RJ7XNqxvIwMYxe1wEyN1KMZnc6N1g03kklyOfdvMz/Image.png)

**Application**

Hosted on a VPS on Hetzner.

Frontend, Backend and Database virtualized in Docker Containers (see Section "CI/CD"), with Ports exposed: 4000 for Backend, 3000 for Frontend.

**Data**

Images are hosted on the Hetzner Object Storage service. It is accessible through S3 clients.

**Reverse Proxy**

Nginx Reverse Proxy setup, routing https traffic from the two domains to the ports.
Two configs:

- api.etter.app → 4000
- etter.app → 3000

In the nginx configs i utilize the Origin Certificates provided by Cloudflare to enable SSL between the VPS and the Cloudflare Reverse Proxy.

**Domain Hosting**

Domains registered on cloudflare. A and AAAA records point to hetzner VPS.
All Traffic goes through full strict ssl encryption (traffic from browser to cloudflare and traffic from cloudflare to vps encrypted).

---

13. CI/CD

I implemented a couple of measures to speed up the process of getting updates up and running consistently.
With my last projects, I avoided Docker, instead cloning repos, and setting up automated pulls on commits to main and building on the EC2 Containers directly. There were issues where code would not run on the EC2 machine because a TypeScript transpiling failed, or other steps during the build process. Using Docker instead would allow me to handle the build process outside of the production environment, mitigating issues and preventing downtime, allowing rollback to previous builds easily, and generally less dependence on the VPS's OS. I went for GitHub Actions to automate Docker processes as it integrates well with GitHub Repos. But I'm considering moving away to a platform like Gitlab when our team grows because it has better support for CI/CD.

**Containerization with Docker**

Both the Front- and Backend have Dockerfiles with multi-stage build processes:

```other
FROM node:alpine AS builder

WORKDIR /backend
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM node:alpine AS production

WORKDIR /backend
COPY package*.json ./

RUN npm ci --omit=dev

COPY --from=builder /backend/dist ./dist
[...]
EXPOSE 55116
CMD ["node", "dist/index.js"]
```

The builder stage is used for building a full, non-downsized container with all dependencies. Then the project is built into the /dist folder. The production stage then takes the dist folder and package.json, and installs only the necessary dependencies needed for production.
This ensures a smaller Docker image size.

**Github Actions**

To ensure automatic building of containers, I set up two Github Action scripts per repository.

The first step executes on a merge or push into the main branch and builds and pushes the image to ghcr.io. It needs to use QEMU as the VPS runs arm:

```yaml
name: Build and Push Image

env:
  IMAGE_NAME: ghcr.io/leifetter/abipulli-backend

on:
  push:
    branches: ["main"]

jobs:
  build:
    runs-on: ubuntu-latest

    permissions:
      packages: write
      contents: read

    steps:
      - uses: actions/checkout@v4

      - name: Set up QEMU
        uses: docker/setup-qemu-action@v3

      - name: Login to GHCR
        uses: docker/login-action@v3
        with:
          registry: ghcr.io
          username: ${{ github.actor }}
          password: ${{ secrets.GHCR_PUSH_TOKEN }}

      - name: Build and push Arm64 image
        uses: docker/build-push-action@v5
        with:
          context: .
          file: ./Dockerfile
          push: true
          platforms: linux/arm64
          tags: ${{ env.IMAGE_NAME }}:latest
          build-args: |
            VITE_API_URL=https://api.etter.app
```

The second script runs when the first script completes, and uses ssh to connect to the VPS using an account "deploy-abipulli" with tightly scoped permissions. It then pulls the imge from ghcr.io and runs it using the local docker-compose file:

```yaml
name: Pull and Run Image

on:
  workflow_run:
    workflows: ["Build and Push Image"]
    types:
      - completed

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repo
        uses: actions/checkout@v3

      - name: Setup SSH
        uses: webfactory/ssh-agent@v0.9.0
        with:
          ssh-private-key: ${{ secrets.HETZNER_KEY }}

      - name: Deploy to VPS
        run: |
          ssh -o StrictHostKeyChecking=no ${{ secrets.HETZNER_USER }}@${{ secrets.HETZNER_HOST }} << 'EOF'
            set -e
            cd /home/deploy-abipulli/projects/
            docker login ghcr.io -u ${{ secrets.GHCR_USERNAME }} -p ${{ secrets.GHCR_TOKEN }}
            docker compose pull
            docker compose down --remove-orphans
            docker compose up -d --build --remove-orphans
          EOF
```

The docker-compose.yml file executed in the second script is comprised of 3 services: A database service using a volume "db_data" (ensuring persistent storage of database contents), the backend and the frontend. For supplying the environment variables they access the env files in /env.

```yaml
services:
  db:
    image: postgres
    environment:
      POSTGRES_USER: ...
      POSTGRES_PASSWORD: ...
      POSTGRES_DB: abipulli
    volumes:
      - db_data:/var/lib/postgresql/data
    ports:
      - 127.0.0.1:5433:5432
  backend:
    image: ghcr.io/leifetter/abipulli-backend:latest
    env_file: ./env/backend.env
    environment:
      DATABASE_URL: postgresql://.../abipulli
      NODE_ENV: production
    depends_on:
      - db
    ports:
      - 4000:55116
  frontend:
    image: ghcr.io/leifetter/abipulli-frontend:latest
    environment:
      VITE_API_URL: https://api.etter.app
    ports:
      - 3000:3000

volumes:
  db_data:
```

There is also another Github Actions script that builds a container upon pull request. I use this to test if the container builds successfully before merging, to prevent a broken container being pushed to the frontend.
Ideally I should also run tests on this container in Github Actions. I will implement this later on when I build out my test suite.

14. Security

This section is a very simplified version of a threat model. I have found a lot of benefits in conducting threat models to analyze possible security leaks.
In the following Graph the possible attack vectors can be seen:

![Image.png](https://resv2.craft.do/user/full/b0e62220-21e7-3e79-e368-d4886dca007e/doc/577C9F7A-056A-4AAE-AD89-A609725DF83A/CAAF8CA3-D192-4BE1-A02D-0089F13AB4F4_2/9T84jraPYVlfgVt6o63pdleOognbH5PuaQvcTx4NAgcz/Image.png)

These tables enumerate vulnerabilities and measures taken to prevent exploitation. They are grouped by Threat Categories:

#### Threat: Direct Access to VPS

| **Vulnerability**                                       | **Prevention**                                           | Examples                                                        |
| ------------------------------------------------------- | -------------------------------------------------------- | --------------------------------------------------------------- |
| Unsafe Authentication                                   | RSA-Level SSH Keys and "PasswordAuthentication" disabled |                                                                 |
| Exposed Keys                                            | Password Encryption on Stored SSH Keys                   |                                                                 |
| (Once Access Acquired) Access to other resources in VPS | SSH Keys for tightly scoped profiles                     | SSH User for Github Actions can only pull and run docker images |

**Threat: SQL Injection**

| Vulnerability              | Prevention                                              |              |
| -------------------------- | ------------------------------------------------------- | ------------ |
| Missing SQL Escaping       | Drizzle ORM automatically escapes SQL injection         |              |
| Missing Request Validation | Zod schemas are used to safeParse all incoming requests | Example File |

**Threat: Code Injection**

| Vulnerability                    | Prevention                                                  |                              |
| -------------------------------- | ----------------------------------------------------------- | ---------------------------- |
| Code passed throguh Input Fields | \- nature of JSX<br/>- zod validation<br/>- use of sanitize | sanitize and sanitizeElement |

#### Threat: Request Interception

| Vulnerability      | Prevention                                                         | Examples     |
| ------------------ | ------------------------------------------------------------------ | ------------ |
| Unsafe HTTP Method | Full-Strict HTTPS from Client to VPS using Cloudflare Origin Certs |              |
| Security Headers   | Use of proper security headers in nginx conf                       | Example file |

#### Threat: General Github (Repository, Actions, GHCR.io) Access

| **Vulnerability**                                   | **Prevention**                                                        | Examples   |
| --------------------------------------------------- | --------------------------------------------------------------------- | ---------- |
| Access to Github                                    | Password + 2FA                                                        |            |
| Exposed Keys in Public Repository                   | Keys stored in .env files                                             |            |
| Access to Keys through Github Actions               | SSH Keys with tightly scoped permissions stored in Github Environment |            |
| Retrieval of Keys from Containers hosted on GHCR.io | Only inject keys when running container on VPS                        | Dockerfile |

#### Threat: Endpoint Exploitation

| Vulnerability                           | Prevention                                                                                                       |            |
| --------------------------------------- | ---------------------------------------------------------------------------------------------------------------- | ---------- |
| Improper Authentication                 | JWT Tokens that store user id's                                                                                  |            |
| Improper Authorization                  | minRole Middleware for checking user id against role db                                                          | minRole.ts |
| Fuzzing                                 | \- Cloudflare Proxy to prevent bot activity<br/>- Cloudlfare logs to monitor<br/>- Russia/China Activity Blocked |            |
| Bruteforce                              | Cloudflare ip request limiting                                                                                   |            |
| Exploitation during development/testing | Cloudflare block requests from all IP's except for own IP                                                        | Example    |

#### Threat: General NPM Vulnerabilities

| Vulnerability                                      | Prevention                                                                                                                                                                       | Example     |
| -------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| Leaking of Credentials from Custom NPM package     | don't store credentials in npm package                                                                                                                                           |             |
| Vulnerability through installed 3rd party packages | \- Periodic npm vulnerability analysis<br/>- Never rely on typing out npm packages (always copy)<br/>- Version Lock all Packages<br/>- Cross reference packages for authenticity | `npm audit` |

#### Threat: User Impersonation

| **Vulnerability**                                          | **Prevention**                                 | **Example**     |
| ---------------------------------------------------------- | ---------------------------------------------- | --------------- |
| User accesses 3rd party Site that sends request to backend | Cors                                           | cors setup file |
| XSS Attack/Token Theft                                     | Use of httponly cookies for storing JWT Tokens | httponly setup  |
| CSRF Attack                                                | httponly, secure and samesite options          | res.cookie      |

#### Threat: DoS

| Vulnerability    | Prevention                       |            |
| ---------------- | -------------------------------- | ---------- |
| Request Spamming | Cloudflare DoS Prevent           |            |
| File Bloating    | Upload Limits for Files          |            |
| JSON Bloating    | Set General MaxSize for requests | 100kb rule |

15. Accessibility/SEO

I implemented a couple of things to allow screen readers to properly scan the application.
Firstly, the nature of routers helps both in accessibility, as it provides a semantic label for each page, and SEO, as it helps scanners index the pages.
Additionally I converted a lot of `div`s into html components such as `<main>` to indicate the central place for content, `<header>` for titles and header data, `<section>` for better partioning, `<form>` for pages with multiple inputs, `<nav>` for navigation components and `<span>` for organizing content within buttons and links.
Components also have `aria-label`s for defining their purpose, `aria-pressed` to indicate the state of the component, `aria-describedBy`/`aria-labelledby` in cases where other components serve as descriptions, and the `role` attribute.
