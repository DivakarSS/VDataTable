<style scoped>
 th {
        color: white;
        background-color: #3b73b9;
        padding: 3px;
        vertical-align: middle;
    }
</style>
<template>
    <div style="padding: 55px;">
    <v-data-table
      :headers="headers"
      :items="desserts"
      item-value="name"
      show-select
      class="elevation-1"
    >
      <template v-slot:headers="props">
        <tr>
            <th>
                Props Data: {{props}} 
            </th>
            <th v-for="header in headers" :key="header.key">
                {{ header.title }}
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
        "key": "name",
        "title": "Name",
        "column_classes": "vue-tbl-column",
        "filter": true,
        "sortable": true
    },
    {
        "key": "dept",
        "title": "Dept",
        "column_classes": "vue-tbl-column",
        "sortable": true
    },
    {
        "key": "age",
        "title": "Age",
        "column_classes": "vue-tbl-column",
        "filter": "filterBasedOnText1",
        "sortable": true
    },
    {
        "key": "gender",
        "title": "Gender",
        "column_classes": "vue-tbl-column",
        "sortable": true
    }
],
      desserts: [
    {
        "id": 1,
        "name": "Yashwanth",
        "dept": "CX Practice",
        "age": "25",
        "gender": "Male"
    },
    {
        "id": 2,
        "name": "Diva",
        "dept": "CX PRactice",
        "age": "22",
        "gender": "Male"
    },
    {
        "id": 716,
        "name": "Ranga",
        "dept": "CX Practice",
        "age": "22",
        "gender": "Male"
    },
    {
        "id": 717,
        "name": "Vignesh",
        "dept": "CX Practice",
        "age": "23",
        "gender": "Male"
    },
    {
        "id": 718,
        "name": "Gokul",
        "dept": "CX Practice",
        "age": "23",
        "gender": "Male"
    },
    {
        "id": 719,
        "name": "Sidd",
        "dept": "CPQ",
        "age": "22",
        "gender": "Male"
    },
    {
        "id": 720,
        "name": "Ramu",
        "dept": "Logistic",
        "age": "29",
        "gender": "Male"
    },
    {
        "id": 721,
        "name": "Krish",
        "dept": "HR",
        "age": "24",
        "gender": "Male"
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
