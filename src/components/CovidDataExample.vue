  <template>
    <div>
        <div class="columns">
            <div class="column">
        <input type="text" class="input mb-3" v-model="search">
            </div>
            <div class="column is-one-quarter">
        <div class="select">
        <select v-model="sort">
            <option v-for="sorting in sortingFields" :key="sorting.name" :value="sorting">{{sorting.name}}</option>
            </select>
            </div>
            </div>
            </div>
        <div class="columns is-multiline">
            <div class="column is-one-fifth" v-for="country in sortedCountries" :key="country.ID">
                <covid-card :country="country"></covid-card>
            </div>
        </div>
    </div>
</template>
<script>
import CovidCard from './CovidCard.vue'
const axios= require('axios');
export default {
    components: { CovidCard },
    created(){
        axios.get('https://api.covid19api.com/summary').then(response => {
            console.log(response);
            this.countries = response.data.Countries;
        });
    },
    data(){
        return {
            countries: [],
            search: '',
            sort: {field: 'TotalConfirmed', name: 'Total Confirmed ascending', order: 'asc'},
            fields: ['TotalConfirmed', 'TotalDeaths', 'NewConfimed', 'NewDeaths']

        }
    },
    computed: {
        filteredCountries(){
            return this.countries.filter(country =>{
                let partialName = country.Country.substr(0, this.search.length);
                return partialName.toLowerCase() == this.search.toLowerCase();
            });
        },
        sortingFields(){
            let sorting = [];
            this.fields.forEach(field => {
                sorting.push({name: field + ' acending', order:'asc', field: field});
                sorting.push({name: field + ' decending', order:'desc', field: field});
            });
            return sorting;
        },
        sortedCountries(){
            return this.filteredCountries.sort((a, b) => {
                
                if(a[this.sort.field] > b[this.sort.field]){
                    return 1;
                } else if(a[this.sort.field] < b[this.sort.field]){
                    return -1;
                }
                return 0;
            });
        }
    }
}
</script>
<style>
</style>