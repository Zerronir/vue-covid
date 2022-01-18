<template>
    <div>
        <select @change="onChange()"
         v-model="selected" class="form-select mt-10 block w-full p-3 rounded border-solid border-2 border-blue-900 mb-10">
            <option value="0">Select country</option>
            <option v-for="country in countries" :value="country.ID">
                {{ country.Country }}
            </option>
        </select>
    </div>
</template>

<script>
export default {
    name: 'CountrySelect',
    props: ['countries'],
    data() {
        return {
            selected: 0
        }
    },
    methods: {
        onChange() {
            const con = this.countries.find((x) => x.ID === this.selected);
            console.log(con)
            this.$emit('get-country', con)
        }
    }
}
</script>