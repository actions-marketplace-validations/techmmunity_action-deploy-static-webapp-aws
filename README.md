# Github Actions - Deploy Static Webapp to S3 and Invalidates Cloudfront

This is a simple utility to deploy an static webapp to AWS S3 bucket and invalidate a cloudfront id. It is that straightforward.

### Usage:

Just place this in your code underneath your build action within the steps, update the variables and secrets and that is it.

```yaml

name: "Deploy To S3" #set whatever name you want to your github job

on: # set the events you would like to trigger this job
  push:
    branches: [master]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2

      - name: Build
        run: # Build the project

      - name: Deploy application to AWS S3 and invalidate cloudfront cache
        uses: techmmunity/action-deploy-static-webapp-aws@1.0.0
        id: deploy
        with:
          build_path: './path/to/build/folder'
          bucket_name: '<AWS BUCKET NAME>'
          bucket_key: '' # Optional
          distribution_invalidation_path: '/*'
        env:
          DISTRIBUTION_ID: '<DISTRIBUTION ID>'
          AWS_REGION: '<AWS REGION>'
          AWS_ACCESS_KEY_ID: '<AWS_ACCESS_KEY_ID>'
          AWS_SECRET_ACCESS_KEY: '<AWS_SECRET_ACCESS_KEY>'
```
