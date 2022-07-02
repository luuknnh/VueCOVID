<script>
export default {
    name: 'CountrySelect',	
    props: ["countries"],
    data() {
        selected: 0;
    },
    methods: { onChange() {
        const country = this.countries.find((item) => item.ID === this.selected);

        console.log(country)
        this.$emit('get-country', country);
    }
    }
}
</script>

<template>
    <select @change="onChange()" v-model="selected" class="form-select block w-full border p-3 rounded mt-10">
        <option disabled selected>Select your option</option>
        <option v-for="country in countries" :value="country.ID">{{ country.Country }}</option>
    </select>
</template>