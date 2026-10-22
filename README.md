# teamsykmelding-github-actions-workflows

This is a repository for GitHub Actions workflows for teamsykmelding

## 🚀 Usage

### Deploying a Ktor application (jar-app-25.yaml)
<details>
<summary>Detailed instructions</summary>
Add the main `deploy.yaml` with the following:

```yaml
name: Deploy to dev and prod
on: push

permissions:
   actions: read
   contents: write
   security-events: write
   packages: write
   id-token: write

jobs:
  jar-app:
    uses: navikt/teamsykmelding-github-actions-workflows/.github/workflows/jar-app-25.yaml@main
    secrets: inherit
    with:
      app: macgyver
```

</details>

### Deploying a Springboot application (boot-jar-app-25.yaml)
<details>
<summary>Detailed instructions</summary>
Add the main `deploy.yaml` with the following:



```yaml
name: Deploy app to dev and prod
on: push

permissions:
   actions: read
   contents: write
   security-events: write
   packages: write
   id-token: write

jobs:
  jar-app:
    uses: navikt/teamsykmelding-github-actions-workflows/.github/workflows/boot-jar-app-25.yaml@main
    secrets: inherit
    with:
      app: syk-dig-backend
```
</details>   

## 👥 Contact

This project is maintained by [navikt/teamsykmelding](CODEOWNERS)

Questions and/or feature requests?
Please create a [pull request](https://github.com/navikt/teamsykmelding-github-actions-workflows/pulls)

If you work in [@navikt](https://github.com/navikt) you can reach us at the Slack
channel [#team-sykmelding](https://nav-it.slack.com/archives/CMA3XV997)
