+++
title = "Streamlit"
post = ""
weight = 1
+++

Streamlit uses Python to build shareable dashboards without the need for front-end development experience.

Download the `streamlit-consent` template relevant to you data warehouse and copy the unzipped folder to your project directory to get started.

{{% attachments style="blue" %}}
{{% /attachments %}}

{{< tabs groupId="streamlit" >}}

{{% tab name="BigQuery" %}}

#### **Step 1:** Install requirements
Run the command below to install the project requirements and run the virtual environment.

❗❗ **This implementation has been tested with the following dependencies: *python = 3.9.13, streamlit = 1.14.0, google-cloud-bigquery = 3.2.0, pandas = *, pandas-gbq = 0.17.9, pydata-google-auth 1.4.0, plotly = 5.11.0*. If you run into package compatibility issues or encounter any errors try using them to build your own environment.**


```bash
pipenv install
pipenv shell
```

#### **Step 2:** Set-up Database Connection
Open `secrets.toml` and add your BigQuery account and database details.

{{% notice warning %}}
Ensure `secrets.toml` is in `.gitignore` to keep your information safe.
{{% /notice %}}

```toml
# .streamlit/secrets.toml

[gcp_service_account]
type = "xxx"
project_id = "xxx"
private_key_id = "xxx"
private_key = "xxx"
client_email = "xxx"
client_id = "xxx"
auth_uri = "xxx"
token_uri = "xxx"
auth_provider_x509_cert_url = "xxx"
client_x509_cert_url = "xxx"

```
#### **Step 3:** Specify schema
Fill out the schema variable within `Healthcheck_board.py` file. Make sure you specify your custom `derived` schema which will be the source schema for the dashboard.


#### **Step 4:** Run the Streamlit dashboard
Run the command below to run the streamlit locally

```bash
streamlit run Healthcheck_board.py
```

{{% /tab %}}

{{% tab name="Snowflake" %}}

#### **Step 1:** Install requirements
Run the command below to install the project requirements and run the virtual environment.

❗❗ **This implementation has been tested with the following dependencies: *python = 3.9.13, streamlit = 1.13.0, snowflake-connector-python = 2.7.9, pandas = *, plotly = 5.10.0*. If you run into package compatibility issues or encounter any errors try using them to build your own environment.**


```bash
pipenv install
pipenv shell
```

#### **Step 2:** Set-up Database Connection
Open `secrets.toml` and add your Snowflake account and database details. Make sure you specify your custom `derived` schema which will be the source schema for the dashboard.

{{% notice warning %}}
Ensure `secrets.toml` is in `.gitignore` to keep your information safe.
{{% /notice %}}

```toml
# .streamlit/secrets.toml

[snowflake]
user = "xxx"
password = "xxx"
account = "xxx"
database = "xxx"
schema = "xxx"
warehouse = "xxx"
role = "xxx"

```
#### **Step 3:** Run the Streamlit dashboard
Run the command below to run the streamlit locally

```bash
streamlit run Healthcheck_board.py
```

{{% notice tip %}}
In case the dashboard does not load due to errors such as 'This session does not have a current database. Call 'USE DATABASE', or use a qualified name.' a possible workaround is to assign default ROLE to the Snowflake user that could handle this.'
{{% /notice %}}

{{% /tab %}}
{{< /tabs >}}

You will be able to see an interactive dashboard similar to this:

![healthcheck_board](../images/1_healthcheck_board.png?width=100pc)

![changelog_board](../images/2_changelog_board.png?width=100pc)

![general_lookup_board](../images/3_general_lookup_board.png?width=100pc)

![consent_overview_by_users](../images/4_consent_overview_by_users.png?width=100pc)

![cmp_board](../images/5_cmp_board.png?width=100pc)
