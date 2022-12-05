+++
title = "Operate Snowplow Consent module"
weight = 1
post = ""
+++

#### **Step 1:** Enable the optional consent module
As the [advanced-analytics-for-web accelerator](https://docs.snowplow.io/accelerators/web/) is a prerequisite, it is assumed that you already have a dbt project set up to process basic web events.

To enable the optional consent module, add the following code snippet to your dbt_project.yml file:


```yml
models:
  snowplow_web:
    optional_modules:
      consent:
        enabled: true
        bigquery:
          enabled: "{{ target.type == 'bigquery' | as_bool() }}"
        snowflake:
          enabled: "{{ target.type == 'snowflake' | as_bool() }}"
```

#### **Step 2:** Run the package

If it is the first time you would like to process the snowplow_web package then you can run the package the recommended way either through your CLI or from within dbt Cloud with the following command:

```
dbt run --selector snowplow_web
```

However, assuming that you already have a working snowplow_web package and you would like to enable consent tracking and modeling at a later stage, you do not need to rebuild the whole model from scratch. For the least amount of reprocessing impact execute the first run the following way:

```
dbt run -m snowplow_web.base --vars 'snowplow__start_date: <date_when_consent_tracking_starts>'
```
This way only the base module is reprocessed. The web model's update logic will recognize the newly enabled models and backfilling should start between the date you defined within snowplow_start_date and the upper limit defined by the variable `snowplow_backfill_limit_days` that is set for the web model.

`Snowplow: New Snowplow incremental model. Backfilling`

You can overwrite this limit for this backfilling process temporarily while it lasts, if needed:

```
# dbt_project.yml

vars:
  snowplow_web:
    snowplow__backfill_limit_days: 1
```

After this you should be able to see all consent models created and added to the derived.snowplow_web_incremental_manifest table. Any subsequent run from this point onwards could be carried out using the recommended web model running method - using the snowplow_web selector.

```
dbt run --selector snowplow_web
```

As soon as backfilling finishes, running the model results in both the web and the consent models being updated during the same run for the same period, both using the same latest set of data from the `_base_events_this_run` table. Please note that while the backfilling process lasts, no new web events are going to be processed.


