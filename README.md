# Resume Site

Hello! This is my personal resume webistie, hosted on AWS and deployed automatically from this repo.

**Live site:** https://d1z1sk0ochps5.cloudfront.net/

## Tech

- HTML, CSS, and JavaScript (no frameworks or build step)
- AWS S3 for storage (private bucket)
- AWS CloudFront for HTTPS and caching
- GitHub Actions for automatic deployment

## Project structure

```
.
├── index.html                  # Page content
├── style.css                   # Styles
├── script.js                   # Small scripts (footer year)
└── .github/workflows/
    └── deploy.yml              # Deploy pipeline
```

## How it's deployed

Every push to `main` triggers a GitHub Actions workflow that:

1. Authenticates to AWS using OpenID Connect (OIDC), so no long-lived access keys are stored in GitHub
2. Syncs the site files to the S3 bucket
3. Invalidates the CloudFront cache so changes show up within a minute or two

```
GitHub (push to main)
   -> GitHub Actions (OIDC)
   -> S3 bucket (private)
   -> CloudFront (HTTPS) -> visitors
```

## Security notes

- The S3 bucket blocks all public access. Only the CloudFront distribution can read from it, using origin access control (OAC).
- The deploy role can only be assumed by this repo's `main` branch.
- The role's permissions are limited to one bucket and one CloudFront distribution.

## Running locally

Open `index.html` in a browser. No install or build is required.

## Contact

- GitHub: [HomzyCode](https://github.com/HomzyCode)
- LinkedIn: [marcusf0](https://www.linkedin.com/in/marcusf0)