# dbt-sample

### Example is from https://www.youtube.com/watch?v=DzxtCxi4YaA&t=2s

* Create Service account with storage admin and BQ admin permissions

* Upload sample csv to gcs bucket
https://www.kaggle.com/datasets/tunguz/online-retail?resource=download

* Create table in BQ

``` sql
CREATE SCHEMA IF NOT EXISTS `dbt-test-462417.retail`
OPTIONS (
  location = 'US' -- or 'EU', etc.
);

LOAD DATA OVERWRITE retail.raw_invoices
(InvoiceNo STRING, StockCode STRING, Description STRING,
Quantity INT64, InvoiceDate STRING, UnitPrice float64,
CustomerID float64, Country STRING)
FROM FILES (
  format = 'CSV',
  uris = ['gs://raw-data-dbt-ingestion2/Online_Retail.csv'],
  skip_leading_rows = 1 -- Skip header row
  );
```

* Create venv, activate & install dependencies 
``` bash
pip install dbt-bigquery==1.9.2
```

* Install dbt dependencies
``` bash
dbt deps
```

* Run transformations
``` bash
dbt run --profiles-dir . 
```

* Below tables should be created in BQ

![alt text](<Screenshot 2025-06-10 012510.png>)