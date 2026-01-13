# GLOBAL - Affiliate Price Comparison Platform

Multi-platform price comparison website for AliExpress, Temu, and Shein products.

## Features

- **Price Comparison**: Compare prices across AliExpress, Temu, and Shein
- **Automatic Product Ingestion**: 
  - AliExpress via official Affiliate API
  - Temu & Shein via CSV/XML feed import
- **Smart Search**: Typo-tolerant, category-aware search with autocomplete
- **Multi-language**: English and Turkish support
- **Admin Panel**: Manage products, feeds, and API settings

## Tech Stack

- **Frontend**: React 18 + Tailwind CSS + Shadcn/UI
- **Backend**: FastAPI (Python)
- **Database**: MongoDB

## Quick Start

### Prerequisites

- Node.js 18+
- Python 3.10+
- MongoDB 6+

### Installation

1. **Clone and setup backend**:
```bash
cd backend
cp .env.example .env
# Edit .env with your settings
pip install -r requirements.txt
```

2. **Setup frontend**:
```bash
cd frontend
cp .env.example .env
# Edit .env with your backend URL
yarn install
```

3. **Start services**:
```bash
# Terminal 1 - Backend
cd backend
uvicorn server:app --host 0.0.0.0 --port 8001

# Terminal 2 - Frontend
cd frontend
yarn start
```

## Configuration

### Backend (.env)

```env
MONGO_URL=mongodb://localhost:27017
DB_NAME=global_db

# AliExpress Affiliate API
ALIEXPRESS_APP_KEY=your-app-key
ALIEXPRESS_APP_SECRET=your-app-secret
ALIEXPRESS_TRACKING_ID=your-tracking-id
```

### Frontend (.env)

```env
REACT_APP_BACKEND_URL=https://your-domain.com
```

## Product Ingestion

### AliExpress (API)

1. Get API credentials from [AliExpress Affiliate Portal](https://portals.aliexpress.com/)
2. Configure in Admin Panel → Settings
3. Sync via Admin Panel → Sync → AliExpress

### Temu / Shein (Feed Import)

**CSV Format**:
```csv
product_id,product_name,description,image_url,price,original_price,affiliate_url,category,brand,availability
PROD001,Product Name,Description,https://image.url,14.99,29.99,https://affiliate.link,Electronics,Brand,in stock
```

**XML Format**:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<products>
  <item>
    <id>PROD001</id>
    <title>Product Name</title>
    <description>Description</description>
    <image_link>https://image.url</image_link>
    <price>14.99 USD</price>
    <sale_price>29.99 USD</sale_price>
    <link>https://affiliate.link</link>
    <product_type>Electronics</product_type>
    <brand>Brand</brand>
    <availability>in stock</availability>
  </item>
</products>
```

**Import Methods**:
1. **Manual Upload**: Admin Panel → Import → Upload CSV/XML
2. **URL Import**: Configure feed URL in Admin Panel → Feed Config

## API Endpoints

### Products
- `GET /api/products` - List products with filters
- `GET /api/products/{id}` - Get product details
- `GET /api/products/search/suggestions?q=` - Search suggestions

### Admin
- `POST /api/admin/feeds/import` - Upload CSV/XML feed
- `POST /api/admin/feeds/config` - Configure feed URL
- `POST /api/admin/feeds/sync/{platform}` - Trigger platform sync
- `POST /api/admin/feeds/sync-all` - Sync all platforms
- `GET /api/admin/feeds/template/{format}` - Get feed template
- `POST /api/admin/aliexpress/sync` - Sync AliExpress
- `POST /api/admin/settings` - Update API settings

## Deployment

### Docker

```dockerfile
# Backend
FROM python:3.10-slim
WORKDIR /app
COPY backend/requirements.txt .
RUN pip install -r requirements.txt
COPY backend/ .
CMD ["uvicorn", "server:app", "--host", "0.0.0.0", "--port", "8001"]
```

### Environment Variables

| Variable | Description |
|----------|-------------|
| `MONGO_URL` | MongoDB connection string |
| `DB_NAME` | Database name |
| `ALIEXPRESS_APP_KEY` | AliExpress API key |
| `ALIEXPRESS_APP_SECRET` | AliExpress API secret |
| `ALIEXPRESS_TRACKING_ID` | Affiliate tracking ID |
| `REACT_APP_BACKEND_URL` | Backend API URL |

## License

MIT
