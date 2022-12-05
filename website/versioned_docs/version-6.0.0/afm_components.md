---
title: AFM Components
sidebar_label: AFM Components
copyright: (C) 2007-2018 GoodData Corporation
id: version-6.0.0-afm_components
original_id: afm_components
---

> **Warning!** The AFM components are legacy elements from the previous GoodData.UI version and will be deprecated. Charts added after GoodData.UI Version 5.1.0 do not support the AFM components.

The AFM components use the [AFM](50_custom__execution.md) property instead of specific properties such as `measures` or `viewBy` that are used in the visual components.

## Charts

### Parameters

| Name | Required? | Type | Description |
| :--- | :--- | :--- | :--- |
| afm | true | [AFM](50_custom__execution.md) | A combination of attributes, measures, and filters |
| projectId | true | string | The workspace ID |
| resultSpec  | false | [ResultSpec](50_custom__result.md) | The structure of the result data |
| config  | false | [ChartConfig](15_props__chart_config.md) | The chart configuration object |
| sdk | false | SDK | A configuration object where you can define a custom domain and other API options |

### Structure

```javascript
import '@gooddata/react-components/styles/css/main.css';
import { AfmComponents } from '@gooddata/react-components';

const { BarChart } = AfmComponents; // replace BarChart with ColumnChart, LineChart, or PieChart whenever needed

<BarChart
    afm={<afm>}
    projectId="<workspace-id>"
    resultSpec={<resultSpec>}
    config={<chart-config>}
    sdk={<sdk>}
/>
```

### Example

```javascript
import '@gooddata/react-components/styles/css/main.css';
import { AfmComponents } from '@gooddata/react-components';

const { BarChart } = AfmComponents;

<BarChart
    afm={{
        measures: [
            {
                localIdentifier: 'CustomMeasureID',
                definition: {
                    measure: {
                        item: {
                            identifier: '<measure-identifier>' // can be referenced from the exported catalog
                        }
                    }
                },
                alias: 'My Measure'
            }
        ],
        attributes: [
            {
                localIdentifier: 'a1',
                displayForm: {
                    identifier: '<attribute-display-form-identifier>'
                }
            }
        ]
    }}
    projectId="<workspace-id>"
    resultSpec={}
/>
```

## Table

### Parameters

| Name | Required? | Type | Description |
| :--- | :--- | :--- | :--- |
| afm | true | [AFM](50_custom__execution.md) | A combination of attributes, measures, and filters |
| projectId | true | string | The workspace ID |
| resultSpec  | false | [ResultSpec](50_custom__result.md) | The structure of the result data |
| sdk | false | SDK | A configuration object where you can define a custom domain and other API options |

### Structure

```javascript
import '@gooddata/react-components/styles/css/main.css';
import { AfmComponents } from '@gooddata/react-components';

const { Table } = AfmComponents;

<Table
    afm={<afm>}
    projectId="<workspace-id>"
    resultSpec={<resultSpec>}
    sdk={<sdk>}
/>
```

### Example

```javascript
import '@gooddata/react-components/styles/css/main.css';
import { AfmComponents } from '@gooddata/react-components';

const { Table } = AfmComponents;

<Table
    afm={{
        measures: [
            {
                localIdentifier: 'CustomMeasureID',
                definition: {
                    measure: {
                        item: {
                            identifier: '<measure-identifier>' // can be referenced from the exported catalog
                        }
                    }
                },
                alias: 'My Measure'
            }
        ],
        attributes: [
            {
                localIdentifier: 'a1',
                displayForm: {
                    identifier: '<attribute-display-form-identifier>'
                }
            }
        ]
    }}
    projectId="<workspace-id>"
    resultSpec={}
/>
```
