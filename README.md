```md
# 🚀 vercel-render-deploy

**GitHub Action to automatically deploy your frontend to Vercel and backend to Render — in one push.**

This action lets you keep a single repository with:

```

your-repo/
├── frontend/
└── backend/

````

…and deploy both services **automatically** whenever you push to `main`.

---

## ✅ What this action does

On every push to `main`:

- If a **`frontend/` folder exists** → deploys it to **Vercel**
- If a **`backend/` folder exists** → triggers a deploy on **Render**
- If either folder is missing → that step is safely skipped

You deploy by doing only:

```bash
git add .
git commit -m "update"
git push origin main
````

Everything else happens automatically. 🎯

---

# 🧱 One-time Setup (you do this only once per project)

## Step 1 — Create your projects

### **A. Create a Vercel project**

1. Go to: [https://vercel.com/new](https://vercel.com/new)
2. Import the **GitHub repo that contains your `frontend/` folder**
3. Click **Deploy** (even if it fails, the project is created)

### **B. Create a Render service**

1. Go to: [https://dashboard.render.com](https://dashboard.render.com)
2. Create a **Web Service** for your `backend/`
3. Connect your GitHub repo

---

## Step 2 — Add secrets to your repo

Go to:

```
Your Repo → Settings → Secrets & variables → Actions → New repository secret
```

Add the following secrets:

### From **Vercel**

| Secret Name         | Where to find it                                                       |
| ------------------- | ---------------------------------------------------------------------- |
| `VERCEL_TOKEN`      | [https://vercel.com/account/tokens](https://vercel.com/account/tokens) |
| `VERCEL_ORG_ID`     | Project → Settings → General → IDs                                     |
| `VERCEL_PROJECT_ID` | Project → Settings → General → IDs                                     |

### From **Render**

| Secret Name                                   | Where to find it                     |
| --------------------------------------------- | ------------------------------------ |
| `RENDER_SERVICE_ID`                           | Your service → Settings → Service ID |
| `RENDER_API_KEY` *(optional but recommended)* | Profile → API Keys                   |

> ⚠️ **Important:**
> These secrets are **repo-specific**. If you use this action in another repo, you must add the secrets again there.

---

# 🚀 Step 3 — Use this action in any repo

Inside your project repo, create:

```
.github/workflows/deploy.yml
```

Then paste this inside:

```yaml
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

      - name: Use my custom deploy action
        uses: your-username/vercel-render-deploy-action@v1
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          render-api-key: ${{ secrets.RENDER_API_KEY }}
          render-service-id: ${{ secrets.RENDER_SERVICE_ID }}
```

Replace:

```
your-username/vercel-render-deploy-action@v1
```

with your actual GitHub username.

---

# ✅ How deployments work after setup

After this, your workflow is:

1. You push to `main`
2. GitHub Actions runs automatically
3. Frontend goes to **Vercel**
4. Backend deploy is triggered on **Render**
5. You don’t touch any dashboard 🎉

---

# 🛠 Repo structure recommendation

Your repo should ideally look like:

```
my-app/
├── frontend/
│   └── (React / Next / Vite etc.)
├── backend/
│   └── (Node / Flask / FastAPI etc.)
└── .github/
    └── workflows/
        └── deploy.yml
```

---

# 🤝 Want to contribute?

Feel free to fork this repo, improve it, and submit a PR!

---

# ⭐ If this helped you

Give this repo a star ⭐ and use it in your projects!

```
```
