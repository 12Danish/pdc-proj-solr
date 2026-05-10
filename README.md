# Apache Solr E-Commerce Search Platform

A full-text product search engine powered by **Apache SolrCloud** with a **Next.js** web interface featuring faceted navigation, autocomplete suggestions, highlighting, sorting, and pagination.

## Prerequisites

- **Java 11+**
- **Apache Solr 9.8.1 binary release**
- **Node.js 18+** and npm

## Project Structure

- `search-app` - Next.js frontend
- `solr-data/schema.json` - schema fields used by Solr
- `solr-data/products.csv` - product catalog data

## Setup and Run

### 1. Extract Solr

Download the **binary** Solr release, then extract it with:

```cmd
tar -xzf solr-9.8.1.tgz
```

If you downloaded the ZIP version instead, extract it with File Explorer or 7-Zip.

### 2. Start SolrCloud

From the extracted Solr folder, start the cloud example:

```cmd
bin\solr.cmd start -e cloud -noprompt
```

Wait for Solr to finish starting, then confirm the admin UI is available at:

```cmd
http://localhost:8983/solr
```

### 3. Create the Collection

```cmd
bin\solr.cmd create -c products
```

### 4. Load the Schema

Run this from the project root:

```cmd
curl.exe -X POST -H "Content-Type: application/json" "http://localhost:8983/solr/products/schema" --data-binary "@solr-data\schema.json"
```

### 5. Index the Product Data

```cmd
curl.exe -X POST -H "Content-Type: text/csv" "http://localhost:8983/solr/products/update/csv?commit=true" --data-binary "@solr-data\products.csv"
```

### 6. Start the Next.js App

Open a new terminal in the project root, then run:

```cmd
cd search-app
npm install
npm run dev
```

Open:

```cmd
http://localhost:3000
```

## Stop the App

Stop Solr with:

```cmd
bin\solr.cmd stop -all
```

Then stop the Next.js server with `Ctrl+C`.

## Features

- Full-text search with highlighted matching terms
- Autocomplete suggestions
- Faceted navigation by category and brand
- Price range filtering
- In-stock filter
- Sorting by relevance, price, rating, date, and name
- Pagination with URL-based state
- Blue-and-white responsive UI

## Tech Stack

- **Backend / Search Engine**: Apache Solr 9.8.1 in SolrCloud mode
- **Frontend**: Next.js, React, TypeScript
- **Styling**: Vanilla CSS with custom properties
