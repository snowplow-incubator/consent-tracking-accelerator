+++
title = "Modeling"
weight = 3
chapter = true
pre = "2. "
+++

<!-- ### Chapter 3 -->

# Modeling your Data

{{<mermaid>}}
flowchart LR
id1(Track)-->id2(Model)-->id3(Visualise)-->id4(Next steps)
style id1 fill:#f5f5f5,stroke:#333,stroke-width:1px
style id2 fill:#f5f5f5,stroke:#6638B8,stroke-width:3px
style id3 fill:#f5f5f5,stroke:#333,stroke-width:1px
style id4 fill:#f5f5f5,stroke:#333,stroke-width:1px
{{</mermaid >}}

To process raw events created by the Snowplow Enhanced Consent plugin we have included an optional module specifically dedicated to model such events in the [snowplow-web dbt package](https://hub.getdbt.com/snowplow/snowplow_web/latest/)

In this chapter you will learn how to enable and run the consent module within the snowplow-web package.
