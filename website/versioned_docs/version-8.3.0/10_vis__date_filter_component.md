---
id: version-8.3.0-date_filter_component
title: Date Filter
sidebar_label: Date Filter
copyright: (C) 2007-2019 GoodData Corporation
original_id: date_filter_component
---

> **The Date Filter component is in the beta stage.**
>
> The component may be changed in future releases, even in a backward incompatible way.

> **Known issues**:
> - `availableGranularities` in `relativeForm` is ignored. `availableGranularities` from the Date Filter component is used instead.
>   - _This issue may be fixed in one of the future releases. The `availableGranularities` property may be removed from the Date Filter component._

The **Date Filter component** is a dropdown component that lists [date filter options](15_props__date_filter_option.md). You can pass allowed options and a callback function, which receives a list of the selected values when a user clicks **Apply**.

![DateFilter Component](assets/date_filter.png "DateFilter Component")

In the Date Filter component, you can optionally define the following:

* The attribute values that should be selected in the filter by default
* The format in which dates should be displayed

    To define the date format, use any value supported by the [date-fns](https://date-fns.org/docs/format) library.
    ![DateFilter Component with International Date Format](assets/date_filter_international_date_format.png "DateFilter Component with dates are displayed in desired formats")

## Example

In the following example, attribute values are listed and the ```onApply``` callback function is triggered when a user clicks **Apply** to confirm the selection.

```jsx harmony
import React, { Component } from "react";
import { DateFilter } from "@gooddata/sdk-ui-filters";
import { myDateFilterOptions } from "myDateFilterConfiguration";

import "@gooddata/sdk-ui-filters/styles/css/main.css";

const availableGranularities = [
    "GDC.time.month",
    "GDC.time.year",
    "GDC.time.quarter",
    "GDC.time.date"];

const dateFilterOptions = myDateFilterOptions();

export class DateFilterComponentExample extends Component {
    constructor(props) {
        super(props);

        this.state = {
            selectedFilterOption: dateFilterOptions.allTime,
            excludeCurrentPeriod: false,
        };
    }

    onApply = (dateFilterOption, excludeCurrentPeriod) => {
        this.setState({
            selectedFilterOption: dateFilterOption,
            excludeCurrentPeriod,
        });
        // eslint-disable-next-line no-console
        console.log(
            "DateFilterExample onApply",
            "selectedFilterOption:",
            dateFilterOption,
            "excludeCurrentPeriod:",
            excludeCurrentPeriod,
        );
    };

    render() {
        return (
            <div style={{ width: 300 }}>
                <DateFilter
                    excludeCurrentPeriod={this.state.excludeCurrentPeriod}
                    selectedFilterOption={this.state.selectedFilterOption}
                    filterOptions={dateFilterOptions}
                    availableGranularities={availableGranularities}
                    customFilterName="Date filter name"
                    dateFilterMode="active"
                    dateFormat="M/d/yy"
                    onApply={this.onApply}
                />
            </div>
        );
    }
}
```

**NOTE:** For the complete source code, see [Live Examples](https://gdui-examples.herokuapp.com/date-filter-component).

## Properties

| Name | Required? | Type | Description |
| :--- | :--- | :--- | :--- |
| excludeCurrentPeriod | true | boolean | The state of the "Exclude current period" checkbox |
| selectedFilterOption | true | [DateFilterOption](15_props__date_filter_option.md#types-of-DateFilter-options) | The selected filter option |
| filterOptions | true | [DateFilterOptions](15_props__date_filter_option.md#types-of-DateFilter-options) | Available filter options |
| availableGranularities | true | [DateFilterGranularity[]](15_props__date_filter_option.md#date-filter-granularity) | An array of available types of granularity for the Relative Form  |
| customFilterName | false | string | A custom filter label |
| dateFilterMode | true | string | Filter mode; can be `readonly`, `hidden`, or `active` |
| dateFormat | false | string | Date format. Defaults to `MM/dd/yyyy`. For the supported values, see the [date-fns library](https://date-fns.org/docs/format). |
| backend | false | [IAnalyticalBackend](https://sdk.gooddata.com/gooddata-ui-apidocs/docs/sdk-backend-spi.ianalyticalbackend.html) | The object with the configuration related to communication with the backend and access to analytical workspaces |
| workspace | false | string | The [workspace](02_start__execution_model.md#where-do-measures-and-attributes-come-from) ID |
| locale | false | string | The localization of the component. Defaults to `en-US`. For other languages, see the [full list of available localizations](https://github.com/gooddata/gooddata-ui-sdk/blob/master/libs/sdk-ui/src/base/localization/Locale.ts). |
| onApply | true | Function | A callback when the selection is confirmed by the user |
| onCancel | false | Function | A callback when the selection is canceled by the user |
| onOpen | false | Function | A callback when the filter dropdown is opened by the user |
| onClose | false | Function | A callback when the filter dropdown is closed by the user |
