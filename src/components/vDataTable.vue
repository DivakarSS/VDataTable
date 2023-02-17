<template>
    <div style="padding: 55px;">
    <v-data-table
      :headers="headers"
      :items="desserts"
      item-value="name"
      show-select
      class="elevation-1"
    >
      <template v-slot:[`column.id`]="{ column }">
        <tr>
            <th>
                <v-icon icon="mdi-filter-variant"></v-icon>
            </th>
            <th>
                {{ column }}
            </th>
            <th>
                {{ column }}
            </th>
            <th>
                {{ column }}
            </th>
            <th>
                {{ column }}
            </th>
        </tr>
      </template>
    </v-data-table>
</div>
</template>

<script>
import {createApp} from "vue";
import 'vuetify/styles';
import 'vuetify/dist/vuetify.js'
import 'vuetify/components'
import { createVuetify } from 'vuetify';
import { VDataTable }from 'vuetify/labs/components'

const vuetify = createVuetify({});
const app = createApp({});
app.use(vuetify);
  export default {
    data: () => ({
      headers: [
    {
        "key": "component",
        "title": "Component",
        "column_classes": "vue-tbl-column",
        "filter": true,
        "sortable": true
    },
    {
        "key": "combustion",
        "title": "Combustion",
        "column_classes": "vue-tbl-column",
        "sortable": true
    },
    {
        "key": "fuel_type",
        "title": "Fuel Type",
        "column_classes": "vue-tbl-column",
        "filter": "filterBasedOnText1",
        "sortable": true
    },
    {
        "key": "work_scope",
        "title": "Work Scope",
        "column_classes": "vue-tbl-column",
        "sortable": true
    }
],
      desserts: [
    {
        "id": 1,
        "component": "Unit Rotor",
        "combustion": "STD",
        "fuel_type": "Dual Fuel",
        "work_scope": "Unmarry Rotor and Inspect not using"
    },
    {
        "id": 2,
        "component": "Unit Rotor",
        "combustion": "STD",
        "fuel_type": "Dual Fuel",
        "work_scope": "Inspection-Turbine/Compressor not using"
    },
    {
        "id": 716,
        "component": "Turbine Case",
        "combustion": "DLN-1",
        "fuel_type": "Dual Fuel",
        "work_scope": "Non-Standard"
    },
    {
        "id": 717,
        "component": "Turbine Case",
        "combustion": "DLN-1",
        "fuel_type": "Gas Only",
        "work_scope": "Non-Standard"
    },
    {
        "id": 718,
        "component": "Turbine Case",
        "combustion": "DLN-1",
        "fuel_type": "Liquid Only",
        "work_scope": "Non-Standard"
    },
    {
        "id": 719,
        "component": "Unit Rotor",
        "combustion": "STD",
        "fuel_type": "Dual Fuel",
        "work_scope": "Non-Standard"
    },
    {
        "id": 720,
        "component": "Compressor Rotor",
        "combustion": "STD",
        "fuel_type": "Dual Fuel",
        "work_scope": "Non-Standard"
    },
    {
        "id": 721,
        "component": "Turbine Rotor",
        "combustion": "STD",
        "fuel_type": "Dual Fuel",
        "work_scope": "Non-Standard"
    }
],
    }),
    components: {
         VDataTable
        
    },
    defaults: {
    VDataTable: {
      fixedHeader: true,
    },
  },
  }
</script>