<template>
  <main v-if="!loading">
    <DataTitle :text="title" />
    <DataBoxes :stats="stats"/>
    <CountrySelect @getCountry ="getCountry" :countries="countries"/>
    <button @click="onGlobalClick" v-if="stats.Country" class="bg-green-700 text-white p-3 mt-10 focus:outline-none hover:bg-green-600">
      Show Global
    </button>


  </main>
  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      fetching Data
    </div>
  </main>
</template>

<script>
// @ is an alias to /src

import DataTitle from "@/components/DataTitle.vue";
import DataBoxes from "@/components/DataBoxes.vue";
import CountrySelect from "@/components/CountrySelect.vue";
export default {
  name: 'HomeView',
  components: {  
  DataTitle,
  DataBoxes,
  CountrySelect
  },
  data(){
    return{
      loading: true,
      title:"Global",
      dataDate: "",
      stats:{},
      countries:[]
    }
  },
  methods: {
   async fetchCoviddata(){
      const res = await fetch('https://api.covid19api.com/summary');
      const data = await res.json();
      console.log(data);
      
      return data;
    },
    getCountry(country){
      this.stats = country;
      this.title = country.Country
    },
    async onGlobalClick(){
      this.loading = true;
      const data = await this.fetchCoviddata();
      this.title = "Global";
      this.stats = data.Global;
      this.loading= false;
    }
  },
  async created(){
    const data = await this.fetchCoviddata();
    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries,
    this.loading = false;
  }
}
</script>
