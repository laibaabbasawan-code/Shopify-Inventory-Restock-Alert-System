# 🛍️ Shopify Inventory & Restock Alert System
An automated Shopify inventory monitoring system built with n8n Cloud. It regularly fetches Shopify products, checks inventory levels, identifies low-stock items, combines them into a single report using JavaScript, and sends an automated Gmail alert to the store owner for timely restocking.


An automated **Shopify inventory monitoring and restock alert system** built with **n8n Cloud**. The workflow periodically checks products in a Shopify store, identifies items with low stock, creates a consolidated report, and automatically sends an email alert to the store owner.

## 🚀 Project Overview

Manually monitoring inventory can be time-consuming, especially when a store has many products. This automation removes that manual work by regularly checking Shopify inventory and notifying the store owner whenever products reach a defined low-stock threshold.

### 🔄 Workflow

```text
Schedule Trigger
       ↓
Shopify - Get Many Products
       ↓
IF - Check Stock ≤ 5
       ↓
Code - Create One Low-Stock Report
       ↓
Gmail - Send Alert
```

## ⚙️ How It Works

### 1. Schedule Trigger

The workflow runs automatically according to a configured schedule, such as every hour or every day.

### 2. Shopify - Get Many Products

The Shopify node retrieves products from the connected Shopify development store, including their variant and inventory information.

### 3. IF Node

Each product's inventory quantity is checked against the low-stock threshold.

Current condition:

```text
Inventory Quantity ≤ 5
```

Products with stock greater than 5 are ignored, while low-stock products continue through the workflow.

### 4. Code Node — Why Is It Used?

The Code node is an important part of this workflow.

The IF node can produce **multiple low-stock items**. If Gmail were connected directly to the TRUE output, the workflow could process each product separately and potentially send multiple emails.

Instead, the Code node runs **once for all incoming items** and combines all low-stock products into **one report**.

For example:

```text
Bottle Cap — Stock: 0
Water Bottle — Stock: 2
Red Mug — Stock: 4
```

becomes a single report:

```text
⚠️ Shopify Low Stock Alert

Bottle Cap — 0
Water Bottle — 2
Red Mug — 4
```

This allows the store owner to receive **one useful summary email instead of a separate email for every low-stock product**.

The Code node uses JavaScript to collect all incoming items, extract the product name and inventory quantity, and combine them into a single formatted report.

### 5. Gmail

The generated report is automatically sent to the store owner's email address.

Example:

```text
Subject: ⚠️ Shopify Low Stock Alert

Product: Bottle Cap
Stock: 0

Product: Water Bottle
Stock: 2
```

The product names and quantities are completely dynamic, so the email changes automatically whenever the Shopify inventory changes.

## 🧰 Technologies Used

* **n8n Cloud** — Workflow automation
* **Shopify** — Product and inventory data
* **JavaScript** — Data transformation and report generation
* **Gmail** — Automated email notifications

## ✨ Key Features

* Automated inventory monitoring
* Shopify integration
* Configurable low-stock threshold
* Automatic filtering of low-stock products
* Dynamic inventory data
* Consolidated low-stock report
* One email for multiple low-stock products
* Automated Gmail notifications
* No manual inventory checking required

## 🎯 Use Case

This workflow can be useful for Shopify store owners who want to automatically monitor inventory and receive timely restock notifications without manually checking their products every day.

## 📌 Future Improvements

Possible improvements include:

* AI-generated restock recommendations
* Different stock thresholds for different products
* Separate alerts for out-of-stock products
* Daily/weekly inventory summaries
* Google Sheets inventory logging
* Slack or Telegram notifications
* Automatic supplier notifications
* Inventory trend analysis

## 👩‍💻 Author
LAIBA 
Built as a practical **Shopify + n8n automation project** to explore real-world workflow automation, API-based data retrieval, conditional logic, JavaScript data transformation, and automated notifications.
