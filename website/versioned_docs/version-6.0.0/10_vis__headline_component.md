---
title: Headline
sidebar_label: Headline
copyright: (C) 2007-2018 GoodData Corporation
id: version-6.0.0-headline_component
original_id: headline_component
---

Headline shows a single number or compares two numbers.

Headlines have two sections: Measure (primary) and Measure (secondary). You can add one item to each section. If you add two items, the headline also displays the change in percent.

![Headline Component](assets/headline.png "Headline Component")

## Structure

```jsx
import { Headline } from '@gooddata/react-components';

<Headline
    projectId={<workspace-id>}
    primaryMeasure={<measure>}
    sdk={<sdk>}
/>
```

## Example

### Headline with a single measure (primary measure)

```jsx
const measure = {
    measure: {
        localIdentifier: 'franchiseFeesIdentifier',
        definition: {
            measureDefinition: {
                item: {
                    identifier: franchiseFeesIdentifier
                }
            }
        }
    }
};

<Headline
    projectId={workspaceId}
    primaryMeasure={measure}
/>
```

### Headline with two measures (primary and secondary measures)

```jsx
const measure = {
    measure: {
        localIdentifier: 'franchiseFeesIdentifier',
        definition: {
            measureDefinition: {
                item: {
                    identifier: franchiseFeesIdentifier
                }
            }
        }
    }
};

const secondaryMeasure = {
    measure: {
        localIdentifier: 'franchiseFeesAdRoyaltyIdentifier',
        definition: {
            measureDefinition: {
                item: {
                    identifier: franchiseFeesAdRoyaltyIdentifier
                }
            }
        }
    }
};

<Headline
    projectId={workspaceId}
    primaryMeasure={measure}
    secondaryMeasure={secondaryMeasure}
/>
```

## Properties

| Name | Required? | Type | Description |
| :--- | :--- | :--- | :--- |
| projectId | true | string | The workspace ID |
| primaryMeasure | true | [Measure](50_custom__execution.md#measure) | The definition of the primary measure |
| secondaryMeasure | false | [Measure](50_custom__execution.md#measure) | The definition of the secondary measure |
| filters | false | [Filter[]](30_tips__filter_visual_components.md) | An array of filter definitions |
| locale | false | string | The localization of the chart. Defaults to `en-US`. For other languages, see the [full list of available localizations](https://github.com/gooddata/gooddata-react-components/tree/master/src/translations). |
| drillableItems | false | [DrillableItem[]](15_props__drillable_item.md) | An array of points and attribute values to be drillable. |
| sdk | false | SDK | A configuration object where you can define a custom domain and other API options |
| ErrorComponent | false | Component | A component to be rendered if this component is in error state. See [ErrorComponent](15_props__error_component.md).|
| LoadingComponent | false | Component | A component to be rendered if this component is in loading state. See [LoadingComponent](15_props__loading_component.md).|
| onError | false | Function | A callback when component updates its error state |
| onLoadingChanged | false | Function | A callback when component updates its loading state |

<!-- These internals are intentionally undocumented
| afterRender | false | Function | A callback after component is rendered |
| dataSource | false | DataSource class | A class that is used to resolve AFM |
| environment | false | string | An Internal property that changes behaviour in Analytical Designer and KPI Dashboards |
| height | false | number | Height of the component in pixels |
| pushData | false | Function | A callback after AFM is resolved |
-->
