<template>
    <div class="grid md:grid-cols-2">
        <div class="shadow-md text-center m-3 rounded bg-blue-100 p-10">
            <h3 class="text-3xl text-blue-900 font-bold mb-4">Cases</h3>
            <div class="text-2xl mb-4">
                <span class="font-bold">New:</span>
                {{ addComma(stats.NewConfirmed) }}
            </div>

            <div class="text-2xl mb-4">
                <span class="font-bold">Total:</span>
                {{ addComma(stats.TotalConfirmed) }}
            </div>
        </div>

        <div class="shadow-md text-center rounded m-3 bg-yellow-100 p-10">
            <h3 class="text-3xl text-yellow-900 font-bold mb-4">Deaths:</h3>
            <div class="text-2xl mb-4">
                <span class="font-bold">New:</span>
                {{ addComma(stats.NewDeaths) }}
            </div>

            <div class="text-2xl mb-4">
                <span class="font-bold">Total:</span>
                {{ addComma(stats.TotalDeaths) }}
            </div>
        </div>

    </div>
</template>

<script>
export default {
    name: 'DataBoxes',
    props: ['stats'],
    methods: {
        addComma(n) {
            return n.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.');
        }
    }
}
</script>