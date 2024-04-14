# Local Installation

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

- Download the git

- Goto Local Folder

  - Docker build of the image

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
