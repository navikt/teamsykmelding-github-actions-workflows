# teamesyfo-github-actions-workflows

This is a repository for GitHub actions workflows for teamesyfo

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
    uses: navikt/teamesyfo-github-actions-workflows/.github/workflows/next-app.yaml@main
    secrets: inherit
    with:
      app: REPLACE_ME
      base-path: REPLACE_ME
```

Add the secondary `demo-delete.yaml` with the following:

```yaml
name: Demo delete
on: delete

jobs:
  branch-delete:
    uses: navikt/teamesyfo-github-actions-workflows/.github/workflows/next-app-demo-delete.yaml@main
    secrets: inherit
    with:
      app: REPLACE_ME
      base-path: REPLACE_ME
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
     namespace: team-esyfo
     labels:
       team: team-esyfo
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

## 👥 Contact

This project is maintained by [navikt/team-esyfo](CODEOWNERS)

If you work in [@navikt](https://github.com/navikt) you can reach us at the Slack
channel [#esyfo](https://nav-it.slack.com/archives/C012X796B4L)
