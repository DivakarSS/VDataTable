<template>

<CDropdown variant="btn-group">
  <CDropdownToggle color="secondary" size="sm">Small button</CDropdownToggle>
  <CDropdownMenu>
    <b-form>
    <label>Filter Columns By:</label>
            <b-form-group label="" >
        <b-form-radio v-model="selectedGridView" value="UnHide">
            UnHide
        </b-form-radio>
        <b-form-radio v-model="selectedGridView" value="Hide">
            Hide
        </b-form-radio>
    </b-form-group>                                                          
</b-form>
  </CDropdownMenu>
</CDropdown>
    <br/>
    <br/>
    <br/>
    <br/>
    <br/>
    <br/>
    <ag-grid-vue
        style="width: 800px; height: 500px"
        class="ag-theme-alpine"
        :columnDefs="columnDefs"
        @grid-ready="onGridReady"
        :rowData="rowData"
        :getRowId="getRowId"
    >
    </ag-grid-vue>
  </template>
  
  <script>
  import "ag-grid-community/styles//ag-grid.css";
  import "ag-grid-community/styles//ag-theme-alpine.css";
  import { AgGridVue } from "ag-grid-vue3";
  import { CDropdown,CDropdownToggle,CDropdownMenu } from '@coreui/vue';
  import '@coreui/coreui/dist/css/coreui.min.css'
  import _ from "underscore";

  export default {
    name: "App",
    components: {
        CDropdown,
        CDropdownToggle,
        CDropdownMenu,
        AgGridVue,
    },
    props:{
        inputScopeViewColumns: { type: String, default: "[]" }
    },
    data: function () {
    return {
      selectedGridView: "",
      scopeViewColumns: [],
      columnDefs: [
    {
        "headerName": "Actions",
        "colId": "_document_number",
        "suppressColumnsToolPanel": true,
        "cellRenderer": "actionCellRenderer",
        "hide": false,
        "suppressMovable": true,
        "lockPinned": true,
        "editable": false,
        "pinned": true,
        "filter": false,
        "sortable": false,
        "suppressSizeToFit": true,
        "width": 110
    },
    {
        "headerName": "Quote Header & Part Description",
        "headerTooltip": "Quote Header & Part Description",
        "children": [{
                "headerName": "#",
                "colId": "_sequence_number",
                "headerTooltip": "#",
                "width": 80,
                "field": "_sequence_number",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": false,
                "sortable": false,
                "readOnly": true,
                "type": "numericColumn"
            },
            {
                "headerName": "Group",
                "colId": "customGroup_line",
                "headerTooltip": "Group",
                "width": 100,
                "field": "customGroup_line.value",
                "filter": "agTextColumnFilter",
                "menuTabs": [],
                "floatingFilter": true,
                "sortable": true,
                "cellEditor": "agRichSelectCellEditor",
                "cellEditorParams": {
                    "values": []
                },
                "modelLevelDisplay": true
            },
            {
                "headerName": "Optional",
                "colId": "options_line",
                "headerTooltip": "Optional",
                "width": 100,
                "field": "options_line",
                "sortable": true,
                "menuTabs": [],
                "floatingFilter": true,
                "readOnly": false,
                "filter": "agSetColumnFilter",
                "cellEditor": "checkboxCellEditor",
                "showSwitchAllValuesMenu": true,
                "fullyEditable": true,
                "pricingView": "Expanded"
            },
            {
                "headerName": "Select Partial Lines",
                "colId": "selectPartialLines_transactionalFlow_line",
                "headerTooltip": "Select Partial Lines",
                "width": 100,
                "field": "selectPartialLines_transactionalFlow_line",
                "sortable": true,
                "menuTabs": [],
                "floatingFilter": true,
                "readOnly": false,
                "headerComponentParams": {
                    "menuIcon": "fa-cog"
                },
                "filter": "agSetColumnFilter",
                "sortable": true,
                "cellEditor": "checkboxCellEditor",
                "showSwitchAllValuesMenu": true,
                "fullyEditable": true
            },
            {
                "headerName": "Locked",
                "colId": "locked_line",
                "headerTooltip": "Locked",
                "width": 100,
                "field": "locked_line",
                "menuTabs": [],
                "floatingFilter": true,
                "sortable": true,
                "readOnly": true,
                "filter": "agSetColumnFilter"
            },
            {
                "headerName": "BOM #",
                "colId": "boM_Number_line",
                "headerTooltip": "BOM #",
                "field": "boM_Number_line",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "readOnly": true
            },
            {
                "headerName": "GE S/N",
                "colId": "gESN",
                "headerTooltip": "GE S/N",
                "field": "gESN",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "readOnly": true
            },
            {
                "headerName": "Equipment SYS ID",
                "colId": "equipmentSystemId_alstom_line",
                "headerTooltip": "Equipment SYS ID",
                "field": "equipmentSystemId_alstom_line",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "readOnly": true
            },
            {
                "headerName": "ERP Quote Number",
                "colId": "alphaQuoteNumber_line",
                "headerTooltip": "ERP Quote Number",
                "width": 100,
                "field": "alphaQuoteNumber_line",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "readOnly": true
            },
            {
                "headerName": "ERP Line #",
                "colId": "gELineNumber_Parts_line",
                "headerTooltip": "ERP Line #",
                "width": 100,
                "field": "gELineNumber_Parts_line",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": false,
                "sort": "asc",
                "sortable": true,
                "unSortIcon": true,
                "suppressSizeToFit": true,
                "readOnly": true
            },
            {
                "headerName": "Part Number",
                "colId": "partNumber_line",
                "field": "partNumber_line",
                "headerTooltip": "Part Number",
                "width": 150,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "readOnly": true
            },
            {
                "headerName": "Part Sent To ERP",
                "colId": "partSentToAlpha_line",
                "field": "partSentToAlpha_line",
                "headerTooltip": "Part Sent To ERP",
                "width": 150,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "readOnly": true,
                "pricingView": "Expanded"
            },
            {
                "headerName": "Description",
                "colId": "_part_desc",
                "headerTooltip": "Description",
                "width": 200,
                "field": "_part_desc",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "readOnly": true
            },
            {
                "headerName": "Customer Line #",
                "colId": "customerLineNumber_line",
                "headerTooltip": "Customer Line #",
                "width": 80,
                "field": "customerLineNumber_line",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agNumberColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "type": "numericColumn"
            },
            {
                "headerName": "Customer Part Number",
                "colId": "customerPartNumber_line",
                "headerTooltip": "Customer Part Number",
                "width": 80,
                "field": "customerPartNumber_line",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true
            },
            {
                "headerName": "Comment",
                "colId": "comments_aqcs_new_line",
                "headerTooltip": "Comment",
                "width": 100,
                "field": "comments_aqcs_new_line",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "readOnly": true
            },
            {
                "headerName": "Original Part",
                "colId": "originalPart_transactionalFlow_line",
                "headerTooltip": "Original Part",
                "width": 100,
                "field": "originalPart_transactionalFlow_line",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "readOnly": true
            }
        ]
    },
    {
        "headerName": "Cost, Price, Deviation",
        "headerTooltip": "Cost, Price, Deviation",
        "children": [{
                "headerName": "Qty",
                "colId": "qty_transactionalFlow_line",
                "headerTooltip": "Qty",
                "width": 80,
                "field": "qty_transactionalFlow_line",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agNumberColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "type": "numericColumn"
            },
            {
                "headerName": "Unit of Measure",
                "colId": "unitOfMeasure_transactionalFlow_line",
                "headerTooltip": "Unit of Measure",
                "width": 100,
                "field": "unitOfMeasure_transactionalFlow_line",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "modelLevelBlank": true,
                "readOnly": true
            },
            {
                "headerName": "Family Code",
                "colId": "familyCode_line",
                "headerTooltip": "Family Code",
                "width": 100,
                "field": "familyCode_line",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "modelLevelBlank": true,
                "readOnly": true
            },
            {
                "headerName": "Cost Class",
                "colId": "costClass_line",
                "headerTooltip": "Cost Class",
                "width": 120,
                "field": "costClass_line",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "readOnly": true
            },
            {
                "headerName": "ERP Status",
                "colId": "eRPLineStatus_transactionalFlow_line",
                "headerTooltip": "ERP Status",
                "width": 100,
                "field": "eRPLineStatus_transactionalFlow_line",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "readOnly": true
            },
            {
                "headerName": "Unit Cost",
                "colId": "unitCost_transactionalFlow_line",
                "headerTooltip": "Unit Cost",
                "field": "unitCost_transactionalFlow_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agNumberColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true
            },
            {
                "headerName": "Line Cost",
                "colId": "costGrid_line",
                "headerTooltip": "Line Cost",
                "field": "costGrid_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agNumberColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true
            },
            {
                "headerName": "Unit List Price",
                "colId": "unitListPrice_transactionalFlow_line",
                "headerTooltip": "Unit List Price",
                "field": "unitListPrice_transactionalFlow_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agNumberColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true
            },
            {
                "headerName": "List Price",
                "colId": "listPriceForParts__transactionalFlow_line",
                "headerTooltip": "List Price",
                "field": "listPriceForParts__transactionalFlow_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agNumberColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true
            },
            {
                "headerName": "Line Price Adjust",
                "colId": "modelOrLineDiscount",
                "headerTooltip": "Line Price Adjust",
                "width": 100,
                "field": "modelOrLineDiscount",
                "menuTabs": [],
                "floatingFilter": true,
                "headerComponentParams": {
                    "menuIcon": "fa-cog"
                },
                "filter": "agSetColumnFilter",
                "sortable": true,
                "cellEditor": "checkboxCellEditor",
                "showSwitchAllValuesMenu": true,
                "modelLevelDisplay": true,
                "readOnly": false
            },
            {
                "headerName": "Unit Target Price",
                "colId": "targetUnitPrice_line",
                "headerTooltip": "Unit Target Price",
                "width": 100,
                "field": "targetUnitPrice_line.value",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agNumberColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true,
                "dealComponentProperty": "finalUnitTargetPrice"
            },
            {
                "headerName": "Line Target Price",
                "colId": "targetLinePrice_line",
                "headerTooltip": "Line Target Price",
                "width": 100,
                "field": "targetLinePrice_line.value",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agNumberColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true,
                "dealComponentProperty": "finalExtendedUnitTargetPrice"
            },
            {
                "headerName": "Unit Selling Price",
                "colId": "unitSellingPrice_transactionalFlow_line",
                "headerTooltip": "Unit Selling Price",
                "width": 100,
                "field": "unitSellingPrice_transactionalFlow_line.value",
                "type": "numericColumn",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agNumberColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "readOnly": false
            },
            {
                "headerName": "Line Selling Price",
                "colId": "extendedDiscount_line",
                "headerTooltip": "Line Selling Price",
                "width": 100,
                "field": "extendedDiscount_line.value",
                "type": "numericColumn",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agNumberColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "readOnly": false
            },
            {
                "headerName": "Currency",
                "colId": "currency_line",
                "headerTooltip": "Currency",
                "field": "currency_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "readOnly": true
            },
            {
                "headerName": "CM%",
                "colId": "cMGrid_line",
                "headerTooltip": "CM%",
                "field": "cMGrid_line",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "readOnly": true,
                "type": "numericColumn"
            },
            {
                "headerName": "Dev from Target Price (%)",
                "colId": "deviationFromTargetPrice_line",
                "headerTooltip": "Dev from Target Price (%)",
                "width": 100,
                "field": "deviationFromTargetPrice_line",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agNumberColumnFilter",
                "sortable": true,
                "type": "numericColumn",
                "readOnly": true
            },
            {
                "headerName": "Ceiling Price",
                "colId": "ceilingLinePrice_line",
                "headerTooltip": "Ceiling Price",
                "field": "ceilingLinePrice_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agNumberColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true,
                "pricingView": "Expanded"
            },
            {
                "headerName": "Item Cost (USD)",
                "colId": "itemCostUSD_line",
                "headerTooltip": "Item Cost (USD)",
                "field": "itemCostUSD_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agNumberColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true
            },
            {
                "headerName": "Line Cost (USD)",
                "colId": "lineCostUSD_line",
                "headerTooltip": "Line Cost (USD)",
                "field": "lineCostUSD_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agNumberColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true
            },
            {
                "headerName": "Unit List Price (USD)",
                "colId": "unitListPriceUSD_line",
                "headerTooltip": "Unit List Price (USD)",
                "field": "unitListPriceUSD_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agNumberColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true
            },
            {
                "headerName": "Line List Price (USD)",
                "colId": "lineListPriceUSD_line",
                "headerTooltip": "Line List Price (USD)",
                "field": "lineListPriceUSD_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agNumberColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true
            },
            {
                "headerName": "Unit Target Price (USD)",
                "colId": "unitTargetPriceUSD_line",
                "headerTooltip": "Unit Target Price (USD)",
                "field": "unitTargetPriceUSD_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agNumberColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true
            },
            {
                "headerName": "Line Target Price (USD)",
                "colId": "targetPriceUSD_line",
                "headerTooltip": "Line Target Price (USD)",
                "field": "targetPriceUSD_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agNumberColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true
            },
            {
                "headerName": "Unit Selling Price (USD)",
                "colId": "unitSellingPriceUSD_line",
                "headerTooltip": "Unit Selling Price (USD)",
                "field": "unitSellingPriceUSD_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agNumberColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true
            },
            {
                "headerName": "Line Selling Price (USD)",
                "colId": "lineSellingPriceUSD_line",
                "headerTooltip": "Line Selling Price (USD)",
                "field": "lineSellingPriceUSD_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agNumberColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true
            },
            {
                "headerName": "Ceiling Price (USD)",
                "colId": "ceilingLinePriceUSD_line",
                "headerTooltip": "Ceiling Price (USD)",
                "field": "ceilingLinePriceUSD_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agNumberColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true
            },
            {
                "headerName": "Last Price Ordered By Customer (USD)",
                "colId": "lastPriceOrderedByCustomerFromOrderData_line",
                "headerTooltip": "Last Price Ordered By Customer (USD)",
                "field": "lastPriceOrderedByCustomerFromOrderData_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "readOnly": true,
                "dealComponentProperty": "lastPricePaidByCustomerFromOrderData"
            },
            {
                "headerName": "Global P50 (USD)",
                "colId": "globalAverage_line",
                "headerTooltip": "Global P50 (USD)",
                "field": "globalAverage_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true,
                "dealComponentProperty": "globalAverage"
            },
            {
                "headerName": "Regional P50 (USD)",
                "colId": "regionalAverage_line",
                "headerTooltip": "Regional P50 (USD)",
                "field": "regionalAverage_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true,
                "dealComponentProperty": "regionalAverage"
            },
            {
                "headerName": "Sub-Regional P50 (USD)",
                "colId": "subRegionalAverage_line",
                "headerTooltip": "Sub-Regional P50 (USD)",
                "field": "subRegionalAverage_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true,
                "hide": true,
                "dealComponentProperty": "subRegionalAverage"
            },
            {
                "headerName": "Customer Historical P50 (USD)",
                "colId": "customerHistoricalAverage_line",
                "headerTooltip": "Customer Historical P50 (USD)",
                "field": "customerHistoricalAverage_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true,
                "dealComponentProperty": "customerHistoricalAverage"
            },
            {
                "headerName": "Global P50 by Frame and Family (USD)",
                "colId": "globalP50ByFrameAndFamily_line",
                "headerTooltip": "Global P50 by Frame and Family (USD)",
                "field": "globalP50ByFrameAndFamily_line",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "type": "numericColumn",
                "cellRenderer": "currencyRenderer",
                "readOnly": true,
                "dealComponentProperty": "globalP50byFrameAndFamily"
            },
            {
                "headerName": "Global P75 by Frame and Family (USD)",
                "colId": "globalP75ByFrameAndFamily_line",
                "headerTooltip": "Global P75 by Frame and Family (USD)",
                "field": "globalP75ByFrameAndFamily_line",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "type": "numericColumn",
                "cellRenderer": "currencyRenderer",
                "readOnly": true,
                "dealComponentProperty": "globalP75byFrameAndFamily"
            },
            {
                "headerName": "Regional P50 by Frame and Family (USD)",
                "colId": "regionalP50ByFrameAndFamily_line",
                "headerTooltip": "Regional P50 by Frame and Family (USD)",
                "field": "regionalP50ByFrameAndFamily_line",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "type": "numericColumn",
                "cellRenderer": "currencyRenderer",
                "readOnly": true,
                "dealComponentProperty": "regionalP50byFrameAndFamily"
            },
            {
                "headerName": "Regional P75 by Frame and Family (USD)",
                "colId": "regionalP75ByFrameAndFamily_line",
                "headerTooltip": "Regional P75 by Frame and Family (USD)",
                "field": "regionalP75ByFrameAndFamily_line",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "type": "numericColumn",
                "cellRenderer": "currencyRenderer",
                "readOnly": true,
                "dealComponentProperty": "regionalP75byFrameAndFamily"
            }
        ]
    },
    {
        "headerName": "Percentiles & Historical values",
        "headerTooltip": "Percentiles & Historical values",
        "children": [
            {
                "headerName": "Price Realization Selling Price (USD)",
                "colId": "priceRealizationSellingPrice_line",
                "headerTooltip": "Price Realization Selling Price (USD)",
                "width": 100,
                "field": "priceRealizationSellingPrice_line.value",
                "type": "numericColumn",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agNumberColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "readOnly": true
            },
            {
                "headerName": "Last Price Ordered by Customer",
                "colId": "lastPriceOrderedByCustomerLC_line",
                "headerTooltip": "Last Price Ordered by Customer",
                "field": "lastPriceOrderedByCustomerLC_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "readOnly": true,
                "hide": true,
                "multiplier": "lastPricePaidByCustomerFromOrderData"
            },
            {
                "headerName": "Date of Last Order By Customer",
                "colId": "dateOfLastOrder_line",
                "headerTooltip": "Date of Last Order By Customer",
                "width": 100,
                "field": "dateOfLastOrder_line",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agDateColumnFilter",
                "sortable": true,
                "readOnly": true,
                "dealComponentProperty": "dateOfLastPurchase",
                "cellRenderer": "dateFormatter",
                "pricingView": "Expanded"
            },
            {
                "headerName": "Quote Conversion Rate",
                "colId": "quoteConversionRate_line",
                "headerTooltip": "Quote Conversion Rate",
                "field": "quoteConversionRate_line",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "type": "numericColumn",
                "readOnly": true,
                "dealComponentProperty": "quoteConversionRate",
                "columnGroupShow": "open"
            },
            {
                "headerName": "Global P50",
                "colId": "globalAverageLC_line",
                "headerTooltip": "Global P50",
                "field": "globalAverageLC_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true,
                "multiplier": "globalAverage"
            },
            {
                "headerName": "Regional P50",
                "colId": "regionalAverageLC_line",
                "headerTooltip": "Regional P50",
                "field": "regionalAverageLC_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true,
                "multiplier": "regionalAverage",
                "pricingView": "Expanded"
            },
            {
                "headerName": "Sub-Regional P50",
                "colId": "subRegionalAverageLC_line",
                "headerTooltip": "Sub-Regional P50",
                "field": "subRegionalAverageLC_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "readOnly": true,
                "multiplier": "subRegionalAverage"
            },
            {
                "headerName": "Customer Historical P50",
                "colId": "customerHistoricalAverageLC_line",
                "headerTooltip": "Customer Historical P50",
                "field": "customerHistoricalAverageLC_line.value",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "cellEditor": "numericEditor",
                "cellRenderer": "currencyRenderer",
                "type": "numericColumn",
                "columnGroupShow": "open",
                "readOnly": true,
                "multiplier": "customerHistoricalAverage"
            },
            {
                "headerName": "Global P50 by Frame and Family",
                "colId": "globalP50ByFrameAndFamilyLC_line",
                "headerTooltip": "Global P50 by Frame and Family",
                "field": "globalP50ByFrameAndFamilyLC_line",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "type": "numericColumn",
                "cellRenderer": "currencyRenderer",
                "readOnly": true,
                "multiplier": "globalP50byFrameAndFamily"
            },
            {
                "headerName": "Global P75 by Frame and Family",
                "colId": "globalP75ByFrameAndFamilyLC_line",
                "headerTooltip": "Global P75 by Frame and Family",
                "field": "globalP75ByFrameAndFamilyLC_line",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "type": "numericColumn",
                "cellRenderer": "currencyRenderer",
                "readOnly": true,
                "hide": true,
                "multiplier": "globalP75byFrameAndFamily",
                "pricingView": "Expanded"
            },
            {
                "headerName": "Regional P50 by Frame and Family",
                "colId": "regionalP50ByFrameAndFamilyLC_line",
                "headerTooltip": "Regional P50 by Frame and Family",
                "field": "regionalP50ByFrameAndFamilyLC_line",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "type": "numericColumn",
                "cellRenderer": "currencyRenderer",
                "readOnly": true,
                "multiplier": "regionalP50byFrameAndFamily"
            },
            {
                "headerName": "Regional P75 by Frame and Family",
                "colId": "regionalP75ByFrameAndFamilyLC_line",
                "headerTooltip": "Regional P75 by Frame and Family",
                "field": "regionalP75ByFrameAndFamilyLC_line",
                "width": 100,
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "type": "numericColumn",
                "cellRenderer": "currencyRenderer",
                "columnGroupShow": "open",
                "readOnly": true,
                "hide": true,
                "multiplier": "regionalP75byFrameAndFamily"
            }
        ]
    },
    {
        "headerName": "Available Qty & Ship Dates",
        "headerTooltip": "Available Qty & Ship Dates",
        "children": [
            {
                "headerName": "Part Lead Time (Bus Weeks Does not include weekends)",
                "colId": "partLeadTimeBusWeeks_line",
                "headerTooltip": "Part Lead Time (Bus Weeks Does not include weekends)",
                "width": 100,
                "field": "partLeadTimeBusWeeks_line",
                "filter": "agTextColumnFilter",
                "sortable": true,
                "menuTabs": [],
                "floatingFilter": true,
                "readOnly": true,
                "pricingView": "Expanded"
            },
            {
                "headerName": "ERP Quote Creation Date",
                "colId": "alphaQuoteCreationDate_transactionalFlow_line",
                "headerTooltip": "ERP Quote Creation Date",
                "width": 100,
                "field": "alphaQuoteCreationDate_transactionalFlow_line",
                "filter": "agDateColumnFilter",
                "sortable": true,
                "menuTabs": [],
                "floatingFilter": true,
                "modelLevelBlank": true,
                "cellRenderer": "dateFormatter",
                "readOnly": true
            },
            {
                "headerName": "ERP Quote Expiration Date",
                "colId": "alphaQuoteExpirationDate_transactionalFlow_line",
                "headerTooltip": "ERP Quote Expiration Date",
                "width": 100,
                "field": "alphaQuoteExpirationDate_transactionalFlow_line",
                "filter": "agDateColumnFilter",
                "sortable": true,
                "menuTabs": [],
                "floatingFilter": true,
                "modelLevelBlank": true,
                "cellRenderer": "dateFormatter",
                "readOnly": true
            },
            {
                "headerName": "Assigned To",
                "colId": "assignedTo_transactionalFlow_line",
                "headerTooltip": "Assigned To",
                "width": 100,
                "field": "assignedTo_transactionalFlow_line",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "columnGroupShow": "open",
                "readOnly": true
            }
        ]
    },
    {
        "headerName": "Technology",
        "headerTooltip": "Technology",
        "children": [{
                "headerName": "Technology",
                "colId": "technology_line",
                "headerTooltip": "Technology",
                "width": 100,
                "field": "technology_line",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "readOnly": true
            },
            {
                "headerName": "Sub Platform",
                "colId": "subPlatform_line",
                "headerTooltip": "Sub Platform",
                "width": 100,
                "field": "subPlatform_line",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "modelLevelBlank": true,
                "readOnly": true,
                "pricingView": "Expanded"
            },
            {
                "headerName": "Business Segmentation",
                "colId": "businessSegmentation_line",
                "headerTooltip": "Business Segmentation",
                "width": 100,
                "field": "businessSegmentation_line",
                "menuTabs": [],
                "floatingFilter": true,
                "filter": "agTextColumnFilter",
                "sortable": true,
                "readOnly": true,
                "pricingView": "Expanded"
            }
        ]
    }
],
      allColumnsIds: [],
      gridApi: null,
      columnApi: null,

      rowData: null,
      getRowId: null,
    };
  },
  created() {
    this.rowData = [
      { id: 'c1', make: 'Toyota', model: 'Celica', price: 35000, dept: 'CSE', year: "I" },
      { id: 'c2', make: 'Ford', model: 'Mondeo', price: 32000, dept: 'EEE', year: "II" },
      { id: 'c8', make: 'Porsche', model: 'Boxster', price: 72000, dept: 'EIE', year: "IV" },
      { id: 'c4', make: 'BMW', model: 'M50', price: 60000, dept: 'ECE', year: "III" },
      { id: 'c14', make: 'Aston Martin', model: 'DBX', price: 190000, dept: 'MECH', year: "IV" },
    ];
    this.getRowId = (params) => params.data.id;
  },

  methods: {
    onGridReady(params) {
      this.gridApi = params.api;
      this.gridColumnApi = params.columnApi;
    },
    

    showColumn(selectedView){
        try{
            let columns = [];
            if(selectedView == "Hide"){
               // columns = ["ag-Grid-AutoColumn",...this.scopeViewColumns]
                columns = ["make","model","id"];
                console.log("columns...",columns);
            }
            else {
                columns = ["make","model","id","dept"];
            }

            let allColumnsfields = ["id","make","model","dept","year","price"]
            let colIdsToHide = _.filter(allColumnsfields, colId => {
                            if(!columns.includes(colId)) {
                                return colId;
                            }
                        });
                    console.log("colIdsToHide...",colIdsToHide);
           
            
                this.gridColumnApi.setColumnsVisible(columns, true);
        
                this.gridColumnApi.setColumnsVisible(colIdsToHide,false);
            
        }
        catch(err){
            console.log("error...",err);
        }
       
        
       
    }
    
  },
  beforeMount(){
    this.scopeViewColumns = JSON.parse(this.inputScopeViewColumns);
    console.log("this.scopeViewColumns in beforeMount...",this.scopeViewColumns);
  },
  watch:{
    selectedGridView: {
        handler(newVal){
            this.scopeViewColumns = JSON.parse(this.inputScopeViewColumns);
            console.log("this.scopeViewColumns in watch...",this.scopeViewColumns);
            this.showColumn(newVal);
        }
    }
  }
};
  </script>
