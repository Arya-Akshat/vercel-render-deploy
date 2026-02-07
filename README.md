# vercel-render-deploy
Github Action Script to automatically deploy on Vercel and Render
Inside any repo, create a file .github/workflows/deploy.yml

and then paste this in it 

name: Deploy

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Use my custom action
      - uses: your-username/vercel-render-deploy-action@v1
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          render-api-key: ${{ secrets.RENDER_API_KEY }}
          render-service-id: ${{ secrets.RENDER_SERVICE_ID }}
