<template>
  <div class="root">
     <!-- <h3>Learn Vue-select</h3>
     <v-select :options ="fruits" ></v-select > <hr/><br/>
     <BFormSelect v-model="selectedTechnology" :options="technologies"
     style="width: 200px; margin-top: 0px; margin-bottom: 0px; margin-right: 10px;"></BFormSelect>
     <hr/><br/>
     <BootstrapModel></BootstrapModel>
     <hr/><br/>
     <BDropdown id="dropdown-1" text="Dropdown Button" class="m-md-2">
      <BDropdownItemButton>UnHide</BDropdownItemButton>
      <BDropdownItemButton>Hide</BDropdownItemButton>
      <BDropdownItemButton>Third Action</BDropdownItemButton>
        <BDropdownDivider></BDropdownDivider>
      <BDropdownItemButton active>Active action</BDropdownItemButton>
      <BDropdownItemButton disabled>Disabled action</BDropdownItemButton>
     </BDropdown>
     <hr/><br/>
     <b-button class="mx-1" @click="check()" variant="success">Success</b-button>
     <hr/><br/> -->
     <!-- <CDropdown variant="btn-group">
<CDropdownToggle color="secondary" size="sm">Small button</CDropdownToggle>
<CDropdownMenu> -->
  <!-- <CDropdownItem>UnHide</CDropdownItem>
  <CDropdownItem>Hide action</CDropdownItem>
  <CDropdownItem >Something else here</CDropdownItem>
  <CDropdownDivider/>
  <CDropdownItem>Separated link</CDropdownItem> -->
  <!-- <b-form>
  <label>Filter Columns By:</label>
          <b-form-group label="" >
      <b-form-radio value="scopeView">
          Scope View
      </b-form-radio>
      <b-form-radio value="erpView">
          ERP View
      </b-form-radio>
  </b-form-group>                                                          
</b-form>
</CDropdownMenu>
</CDropdown> -->
<!-- <hr/><br/> -->
<!-- <AgGrid></AgGrid> -->
<!-- <hr/><br/> -->
<vDataTable/>
  </div>
  
</template>
<script>
//import {createApp} from 'vue'
// import vSelect from "vue-select";
// import BootstrapVue3 from 'bootstrap-vue-3'
// import {BDropdown} from 'bootstrap-vue-3';
// import 'bootstrap/dist/css/bootstrap.css'
// import 'bootstrap-vue-3/dist/bootstrap-vue-3.css'
// import BootstrapModel from './components/bootstrap-model.vue'
// import AgGrid from './components/ag-grid-test.vue'
// import "vue-select/dist/vue-select.css";
// import { CDropdown,CDropdownToggle,CDropdownMenu } from '@coreui/vue';
// import '@coreui/coreui/dist/css/coreui.min.css'
// import 'bootstrap/dist/css/bootstrap.min.css'
import VDataTable from './components/vDataTable.vue'
// console.log("vue-select");
//createApp({}).use(BootstrapVue3);

export default {
  data () {
    return {
      // fruits:["Mangoo","Apple","Orange","Melon","Pineapple","Lecy","Blueberry"],
      // selectedTechnology: "All Technologies",
      // technologies: [
      //         { text: "All Technologies", value: "All Technologies" },
      //         { text: "Gas", value: "Gas" }, 
      //         { text: "Steam", value: "Steam" },
      //         { text: "Generator", value: "Generator" }
      //     ],
    }
  },
  components:{
    // vSelect,
    // BootstrapModel,
    //  BDropdown,
    // CDropdown,
    // CDropdownToggle,
    // CDropdownMenu,
    // AgGrid,
    VDataTable
  },
  methods:{
      check:function(){
        console.log("BButton Working");
      }
  }
}
</script>


<style scoped>
/* @import "vue-select/src/scss/vue-select.scss"; */

/* @import "~vue-select/dist/vue-select.css"; */
/* .root{
    margin: 0 auto;
    max-width: 600px;} */
</style>










