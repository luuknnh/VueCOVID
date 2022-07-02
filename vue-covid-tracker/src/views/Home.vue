<script>
import DataTitle from '../components/DataTitle.vue';
import DataBoxes from '../components/DataBoxes.vue';
import CountrySelect from '../components/CountrySelect.vue';

export default {
    name: 'Home',
    components: {
        DataTitle,
        DataBoxes,
        CountrySelect
    },
    data() {
        return  {        
        loading: true,
        title: 'Global',
        dataDate: '',
        stats: {},
        countries: [],
        loadingImage: import('../assets/loading.gif'),
        }
    },

    methods: {
        async fetchCovidData() {
            const response = await fetch('https://api.covid19api.com/summary');
            const data = await response.json();
            return data
        },
        getCountryData(country) {
            this.title = country.Country;
            this.dataDate = country.Date;
            this.stats = country;
        },
        async clearCountryData() {
           this.loading = true;

           const data = await this.fetchCovidData()
           this.title = 'Global';
           this.stats = data.Global;
           this.loading = false;
        }
    },
    async created() {
        const data =  await this.fetchCovidData();
        this.dataDate = data.Date;
        this.stats = data.Global;
        this.countries = data.Countries;
        this.loading = false;
    },
}
</script>

<template>
    <main v-if="!loading">
        <DataTitle :text="title" :dataDate="dataDate"/>

        <DataBoxes :stats="stats"/>

        <CountrySelect  @get-country="getCountryData" :countries="countries"/>

        <button v-if="stats.Country" 
        @click="clearCountryData"
        class="flex bg-blue-500 text-white rounded p-3 mt-10 focus:outline-none hover:bg-blue-400 justify-center aling-center items-center  ">

            Clear Country
        </button>
    </main>


    <main class="flex flex-col justify-center align-center text-center" v-else>
        <div class="text-gray-500 text-3xl mt-10 mb-6">Fetching Data</div>
        <img v-if="loadingImage = true" src="../assets/loading.gif" class="w-24 m-auto">
    </main>


</template>

