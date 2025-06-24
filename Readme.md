Cost Optimization Challenge: Managing Billing Records in Azure Serverless Architecture.



**Recommended Cost-Optimization Strategy
**
1. Hot–Cold Data Separation
    * Hot Data: Last 3 months → Stored in primary Cosmos DB container (high RUs, fast access).
    * Cold Data: Older than 3 months → Moved to Azure Blob Storage (Cool tier)


**2.	Simplicity & Ease of Implementation – The solution should be straightforward to deploy and maintain.**
      Cosmos DB (billing records)
      Azure Function (processes new records)
      Blob Storage (write to JSON files per month/customer)




**How You Avoid Downtime & Data Loss**
1. Set up Blob Storage for Cold Tier
Define a structure: billing-archive/year=YYYY/month=MM/customer=ID/

Enable soft-delete and lifecycle management policies (for safety)

2. Use Cosmos DB Change Feed + Azure Function
Listen for inserts/updates

If a record is older than 3 months:

Write it to blob (e.g., in JSON format)

Optionally flag the record in Cosmos DB as archived: true (initially keep it)




