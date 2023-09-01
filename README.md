# teamsykmelding-github-actions-workflows

This is a repository for GitHub actions workflows for teamsykmelding

## 🚀 Usage

### Deploying a Next application (next-app.yaml)

Builds 1 app per environment. Supports deploying demo-prefixed branches to their own ingress.

<details>
<summary>Detailed instructions</summary>
Add the main `deploy.yaml` with the following:

```yaml
name: Build & Deploy
on: push

jobs:
  next-app:
    uses: navikt/teamsykmelding-github-actions-workflows/.github/workflows/next-app.yaml@main
    secrets: inherit
    with:
      app: sykmeldinger
      base-path: /syk/sykmeldinger
```

Add the secondary `demo-delete.yaml` with the following:

```yaml
name: Demo delete
on: delete

jobs:
  branch-delete:
    uses: navikt/teamsykmelding-github-actions-workflows/.github/workflows/next-app-demo-delete.yaml@main
    secrets: inherit
    with:
      app: dinesykmeldte
      base-path: /arbeidsgiver/sykmeldte
```

#### **Important:**

This reusable workflows make the following assumptions:

1. There is a `Dockerfile` on root

   This dockerfile NEEDS to accept the argument `ENV` (`ARG ENV`) and copy the following: `COPY nais/envs/.env.$ENV /app/.env.production`

2. The naiserator files are in the `nais` folder, named `nais-dev.yaml`, `nais-demo.yaml` and `nais-prod.yaml`.

   The `nais.demo.yaml` needs to be parameterized with the following:

   ```yaml
   apiVersion: 'nais.io/v1alpha1'
   kind: 'Application'
   metadata:
     name: {{appname}}-demo
     namespace: teamsykmelding
     labels:
       team: teamsykmelding
       branchState: {{branchState}}
   spec:
     image: {{image}}
     port: 3000
     ingresses:
       - {{ingress}}
     replicas:
       min: {{replicas}}
       max: {{replicas}}
   ```

   This is to support deploying branches to their own ingress.

3. There needs to be a `nais/envs` folder with the following files: `.env.dev`, `.env.demo`, `.env.prod`. These envs will be available both during build and runtime.

   Note: Normal runtime-only (e.g. backend-only) envs can still be added in the nais.yaml.
   </details>

### Deploying a Ktor application (jar-app.yaml)
```yaml
name: Deploy to dev and prod
on: push

jobs:
  jar-app:
    uses: navikt/teamsykmelding-github-actions-workflows/.github/workflows/jar-app.yaml@main
    secrets: inherit
    with:
      app: macgyver
```


### Deploying a Springboot application (boot-jar-app.yaml)
```yaml
name: Deploy app to dev and prod
on: push

jobs:
  jar-app:
    uses: navikt/teamsykmelding-github-actions-workflows/.github/workflows/boot-jar-app.yaml@main
    secrets: inherit
    with:
      app: syk-dig-backend
```
   

## 👥 Contact

This project is maintained by [navikt/teamsykmelding](CODEOWNERS)

Questions and/or feature requests?
Please create an [issue](https://github.com/navikt/teamsykmelding-github-actions-workflows/issues)

If you work in [@navikt](https://github.com/navikt) you can reach us at the Slack
channel [#team-sykmelding](https://nav-it.slack.com/archives/CMA3XV997)
