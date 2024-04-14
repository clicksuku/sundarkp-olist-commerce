# sundarkp-olist-commerce
This repository was created to reflect the learning from Data Engineering Zoomcamp 2024 Cohort by me (Sundara Kumar Padmanabhan)

**High Level Design**

<img src="Visualizations/OlistHLD.jpg" style="width:6.26806in;height:3.35764in"
alt="A group of logos on a white background Description automatically generated" />

## Datasets Taken

Brazil Olist Customers, Sellers and Marketing Data

> <https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce?resource=download>
>
> <https://www.kaggle.com/datasets/olistbr/marketing-funnel-olist>

## <img src="Visualizations/OlistDataStructures.jpg" style="width:6.21574in;height:3.74074in"
alt="Data Schema" />

# Run with Docker Mage + BQ & GCS Bucket 

## Perquisites

- Google Project

  - API and Services enabled

- Service Account

  - Goto IAM & Admin. Configure the following Permissions required

    - BigQuery Admin

    - BigQuery Read Session User

    - Compute Storage Admin

    - Owner

    - Storage Admin

    - Storage Folder Admin

    - Storage Object Admin

- Terraform

  - In GCP Cloud Storage, bucket has to be created

  - In BigQuery, Dataset has to be created (olist)

## Preparing the ground

- Git Clone the Repository from
  <https://github.com/clicksuku/sundarkp-olist-commerce.git>

- Build the MAGE_SPARK Image from the DockerFile

  - Docker build -t mage_spark .

## Running it locally

- Create a folder where the mage data is going to reside

- Go to folder

  - Copy the Service Account.JSON here

  - Copy the Kaggle Account.JSON here

  - Copy the Custom Mage Pipeline created for the Project

- Run docker command to initiate mage

> *<span class="mark">docker run -d -t --name skp_mage_spark -e
> SPARK_MASTER_HOST='local' -p 6789:6789 -v \$(pwd):/home/src mage_spark
> /app/run_app.sh mage start skpmagepipeline</span>*

- CD to *skpmagepipeline/dbt*

- Git clone git@github.com:clicksuku/skp_olist_data_dbt.git

- Run <http://localhost:6789/>

- Goto Pipeline skpdezolist

  - Run each step in the pipeline

## Use Cases

- Customer Analytics

  - Customer Life Time Orders Count

  - Customer Life Time Value

  - Date-wise orders of Customers

- Store Analytics

  - Olist Stores Geo Distribution

- Seller Analytics

  - Increase in number of sellers per month

  - Number of new Product categories added per month

  - Categories Purchased at high frequency yearly, monthly

- Marketing Impact on

  - Addition of new Sellers

  - Addition of new Customers

  - Addition of new Orders

- Seller vs Customer spread across states

# 

# Visualizations and Analysis

[Link to Visualizations and Analysis
BI](https://github.com/clicksuku/sundarkp-olist-commerce/blob/main/VisualizationsBI.md)

# References

**Spark Cluster in Docker (Did not use as Spark was creating a Unnamed:0
Column)**

[<u>https://docs.mage.ai/integrations/spark-pyspark#custom-spark-session-at-the-project-level</u>](https://docs.mage.ai/integrations/spark-pyspark#custom-spark-session-at-the-project-level)

[<u>https://medium.com/@MarinAgli1/setting-up-a-spark-standalone-cluster-on-docker-in-layman-terms-8cbdc9fdd14b</u>](https://medium.com/@MarinAgli1/setting-up-a-spark-standalone-cluster-on-docker-in-layman-terms-8cbdc9fdd14b)

**Kaggle Datasets**

[<u>https://medium.com/mcd-unison/using-the-kaggle-api-e43e902fba23</u>](https://medium.com/mcd-unison/using-the-kaggle-api-e43e902fba23)

[<u>https://www.kaggle.com/docs/api</u>](https://www.kaggle.com/docs/api)

**Terraform remote exec -**

<https://medium.com/google-cloud/terraform-remote-exec-on-google-compute-engine-vm-instance-d47def447072>

[<u>https://github.com/Sayed-Imran/Terraform-Scripts</u>](https://github.com/Sayed-Imran/Terraform-Scripts)

[<u>https://github.com/Sayed-Imran/Terraform-Scripts/tree/master/gcp-remote-exec</u>](https://github.com/Sayed-Imran/Terraform-Scripts/tree/master/gcp-remote-exec)

[<u>https://gist.github.com/smford22/54aa5e96701430f1bb0ea6e1a502d23a#file-main-tf</u>](https://gist.github.com/smford22/54aa5e96701430f1bb0ea6e1a502d23a#file-main-tf)
[<u>https://www.devopsschool.com/blog/terrafrom-example-code-for-remote-exec-provisioner/</u>](https://www.devopsschool.com/blog/terrafrom-example-code-for-remote-exec-provisioner/)

**Mage for BigQuery**

[<u>https://github.com/mage-ai/mage-ai/blob/master/mage_integrations/mage_integrations/destinations/bigquery/README.md</u>](https://github.com/mage-ai/mage-ai/blob/master/mage_integrations/mage_integrations/destinations/bigquery/README.md)

[<u>https://datatalks-club.slack.com/archives/C01FABYF2RG/p1711711901567119</u>](https://datatalks-club.slack.com/archives/C01FABYF2RG/p1711711901567119)

# Top Issues

- Kaggle initialisation in Mage Data Loader was an issue

  - Conda was installed in Docker.

  - Kaggle and other Python libraries were installed in the Conda Active
    environment.

  - So when Conda was not installed and python libraries were installed.
    Data Loader was able to find Kaggle

- Spark Initialization in Mage Data Loader was an Issue

  - DockerFile was created using
    [<u>https://medium.com/@MarinAgli1/setting-up-a-spark-standalone-cluster-on-docker-in-layman-terms-8cbdc9fdd14b</u>](https://medium.com/@MarinAgli1/setting-up-a-spark-standalone-cluster-on-docker-in-layman-terms-8cbdc9fdd14b)

  - Spark session had to be initialized using ScratchPad as mentioned in
    [<u>https://docs.mage.ai/integrations/spark-pyspark#custom-spark-session-at-the-project-level</u>](https://docs.mage.ai/integrations/spark-pyspark#custom-spark-session-at-the-project-level)

- BigQuery tables had ‘Unnamed:0’ as index column.

  - Spark Read CSV to PD.DataFrame added an index column.

  - Referring to
    [<u>https://sparkbyexamples.com/pandas/pandas-drop-index-column/</u>](https://sparkbyexamples.com/pandas/pandas-drop-index-column/)
    and
    [<u>https://www.kaggle.com/discussions/general/354943</u>](https://www.kaggle.com/discussions/general/354943),
    following were done to remove index

    - pdf = df.toPandas()

    - pdf2 = pdf.reset_index(drop=True)

