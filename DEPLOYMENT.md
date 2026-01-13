# GLOBAL - Deployment Guide

## Admin Panel Access
- URL: /admin
- Auth: HTTP Basic Authentication
- Default credentials in backend/.env:
  - ADMIN_USERNAME=globaladmin
  - ADMIN_PASSWORD=Gl0b4l$ecure2024!

## Change Admin Password
Edit backend/.env:
```
ADMIN_USERNAME="your_username"
ADMIN_PASSWORD="your_new_password"
```

## Tech Stack
- Frontend: React 18
- Backend: FastAPI (Python)
- Database: MongoDB

## Local Setup

### Backend
```bash
cd backend
pip install -r requirements.txt
# Edit .env with your MongoDB URL
uvicorn server:app --host 0.0.0.0 --port 8001
```

### Frontend
```bash
cd frontend
yarn install
# Edit .env with your backend URL
yarn start
```

## Production Deployment
1. Deploy backend to any Python hosting (Railway, Render, VPS)
2. Deploy frontend to Vercel/Netlify or same server
3. Set environment variables on your hosting platform

## Admin Panel Features
- Dashboard: Product stats
- Feed Import: Upload CSV/XML for Temu/Shein
- API Settings: AliExpress API + Temu/Shein affiliate IDs
- Site Settings: Contact email, site name
- Sync History: Import logs

## Affiliate Links (Temu/Shein)
Upload CSV with this format:
```csv
product_id,product_name,price,original_price,affiliate_url,image_url,category
PROD001,Product Name,14.99,29.99,https://your-affiliate-link,https://image.jpg,Electronics
```
