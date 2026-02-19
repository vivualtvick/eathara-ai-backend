Below is a **clear, structured deployment guide** for deploying your Backend on **Railway** and Frontend on **Vercel**, using **PostgreSQL** and a **Next.js** frontend.

---

# Full Deployment Documentation

---

# Backend Deployment (Railway)

## Step 1: Create a New Project

1. Go to **Railway Dashboard**
2. Click **New Project**
3. Connect and configure your **GitHub** account

---

## Step 2: Add PostgreSQL Database

1. Inside the project, click **Add Service**
2. Select **Database**
3. Choose **PostgreSQL**
4. Wait until the database is provisioned successfully
5. Click on the created **Postgres service**

---

## Step 3: Deploy Backend Service

### 3.1 Create Backend Service

1. Click **Create**
2. Select **Deploy from GitHub Repo**
3. Choose your **Backend repository**

---

### 3.2 Configure Backend Settings

#### A. Set Root Directory

1. Open **Backend Service**
2. Go to **Settings**
3. Navigate to **Services**
4. Click **Add Root Directory**
5. Set root directory to:

```
/root
```

---

#### B. Configure Networking

1. Go to **Networking**
2. Click **Generate Domain**
3. Wait for the public domain to be generated

---

#### C. Configure Build Settings

1. Go to **Build**
2. Select **Builder**
3. Choose **Dockerfile**
4. Set Dockerfile path:

```
/root/Dockerfile
```

---

## Step 4: Configure Environment Variables

### 4.1 Add Database Reference Variables

Go to **Variables → New Variable → Reference**

Add the following variables one by one:

```
PGUSER
PGPASSWORD
PGDATABASE
PGPORT
PGHOST
```

---

### 4.2 Add Raw Variables

Go to **Variables → Raw Editor** and add:

```env
DEBUG="0"
FRONTEND_URL="http://localhost:3000"
CSRF_TRUSTED_ORIGINS="http://localhost:3000"
ALLOWED_HOSTS="localhost"
SECRET_KEY="cbjsdjsjfjknfkjsdjksajdsakfkjaskfjksjkfs"
```

Click **Update Variables**

---

## Step 5: Deploy Backend

1. Click **Deploy**
2. Wait for:

   * Build completion
   * Service to become online

Optional:
You can monitor logs:

* Go to **Deployments**
* Click **View Logs**

  * Build Logs
  * Deploy Logs

---

## Step 6: Copy Backend Public URL

Once deployment is successful:

1. Go to **Service → Settings → Networking**
2. Copy the **Public Networking URL**

You will need this for frontend configuration.

---

# Frontend Deployment (Vercel)

---

## Step 1: Import Frontend Repository

1. Go to **Vercel**
2. Click **Continue with GitHub**
3. Authorize Vercel if prompted
4. Click **Install**
5. Select **Import Project**
6. Choose your **Frontend repository**

---

## Step 2: Configure Project Settings

### 2.1 Application Preset

Select:

```
Next.js
```

---

### 2.2 Set Root Directory

1. Click **Edit** under Root Directory
2. Set directory to:

```
frontend
```

---

### 2.3 Add Environment Variable

Go to **Environment Variables** and add:

```
NEXT_PUBLIC_API_BASE_URL = https://<your-backend-public-url>
```

Example:

```
NEXT_PUBLIC_API_BASE_URL = https://eathara-ai-backend-production.up.railway.app
```

(Use the URL copied from Railway)

---

## Step 3: Deploy Frontend

1. Click **Deploy**
2. Wait until deployment completes

---

# 3️⃣ Final Backend Configuration (Connect Frontend to Backend)

After frontend is deployed:

---

## Step 1: Copy Frontend URL

1. Go to **Vercel Dashboard**
2. Open your project
3. Go to **Domains**
4. Copy the primary frontend URL

Example:

```
https://ethara-ai-frontend.vercel.app
```

---

## Step 2: Update Backend Environment Variables

1. Go to **Railway → Backend Service**
2. Open **Variables**
3. Use **Raw Editor**

Update the following:

```env
FRONTEND_URL="https://ethara-ai-frontend.vercel.app"
CSRF_TRUSTED_ORIGINS="https://ethara-ai-frontend.vercel.app"
ALLOWED_HOSTS="eathara-ai-backend-production.up.railway.app"
```

⚠️ `ALLOWED_HOSTS` should contain only the backend domain (without https).

Click **Update Variables**

---

## Step 3: Redeploy Backend

1. Click **Deploy**
2. Wait for new deployment to complete

---

# Deployment Complete

Your system is now fully deployed:

* Backend hosted on **Railway**
* Database on **PostgreSQL**
* Frontend hosted on **Vercel**
* Environment variables properly configured
* Frontend and backend securely connected

---

# 🔎 Troubleshooting Tips

If something fails:

* Check **Build Logs**
* Check **Deploy Logs**
* Verify environment variables
* Confirm Dockerfile path
* Ensure correct domain in:

  * `FRONTEND_URL`
  * `CSRF_TRUSTED_ORIGINS`
  * `ALLOWED_HOSTS`
  * `NEXT_PUBLIC_API_BASE_URL`

---
