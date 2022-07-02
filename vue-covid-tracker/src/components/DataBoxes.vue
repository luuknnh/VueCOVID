<script>
export default {
    name: 'DataBoxes',
    props: ['stats'],
    methods: {
        numberWithComas(x) {
            return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
        }
    }
}
</script>

<template>
    <div class="grid md:grid-cols-2 gap-4">
        <div class="shadow-md bg-red-100 p-10 text-center rounded">
            <h3 class=" text-3xl text-red-500 font-bold mb-4">Cases</h3>


            <div class="text-2xl mb-4">
                <span class="font-bold">New:</span>
                {{ numberWithComas(stats.NewConfirmed) }}
            </div>
            <div class="text-2xl mb-4">
                <span class="font-bold">Total:</span>
                {{ numberWithComas(stats.TotalConfirmed) }}
            </div>
        </div>

        <div class="shadow-md bg-red-100 p-10 text-center rounded">
            <h3 class=" text-3xl text-red-500 font-bold mb-4">Deaths</h3>


            <div class="text-2xl mb-4">
                <span class="font-bold">New:</span>
                {{ numberWithComas(stats.NewDeaths) }}
            </div>
            <div class="text-2xl mb-4">
                <span class="font-bold">Total:</span>
                {{ numberWithComas(stats.TotalDeaths) }}
            </div>
        </div>
    </div>
</template>