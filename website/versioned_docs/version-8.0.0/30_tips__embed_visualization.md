---
title: Embed an Insight Created in Analytical Designer
sidebar_label: Embed an Insight Created in Analytical Designer
copyright: (C) 2007-2018 GoodData Corporation
id: version-8.0.0-ht_embed_visualization
original_id: ht_embed_visualization
---

To embed an existing insight created in Analytical Designer, use the [InsightView component](10_vis__insight_view.md).

**Steps:**

1. Obtain the identifier of the insight via [catalog-export](gdc_catalog_export).

2. Import the InsightView component from the `@gooddata/sdk-ui-ext` package into your app:
    ```javascript
    import { InsightView } from "@gooddata/sdk-ui-ext";
    ```

3. Create an `InsightView` component in your app, and provide it with the workspace ID and the visualization identifier that you obtained at Step 1:
    ```jsx
    import { InsightView } from "@gooddata/sdk-ui-ext";
    import "@gooddata/sdk-ui-ext/styles/css/main.css";

    <InsightView
        insight="aby3polcaFxy"
        config={{
            colors: ["rgb(195, 49, 73)", "rgb(168, 194, 86)"],
            legend: {
                enabled: true,
                position: "bottom"
            }
        }}
    />
    ```
