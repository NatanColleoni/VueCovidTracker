<template>
    <div class="grid md:grid-cols-2 gap-4">
        <!-- Box 1 -->
        <div class="shadow-md bg-purple-100 p-10 text-center rounded">
            <h3 class="text-3xl text-purple-900 font-bold mb-4">Cases</h3>

            <div class="text-2xl mb-4">
                <span class="font-bold">New:</span>
                {{ numberWithDots(stats.NewConfirmed) }}
            </div>

            <div class="text-2xl mb-4">
                <span class="font-bold">Total:</span>
                {{ numberWithDots(stats.TotalConfirmed) }}
            </div>
        </div>

        <!-- Box2 -->
        <div class="shadow-md bg-purple-100 p-10 text-center rounded">
            <h3 class="text-3xl text-purple-900 font-bold mb-4">Deaths</h3>

            <div class="text-2xl mb-4">
                <span class="font-bold">New:</span>
                {{ numberWithDots(stats.NewDeaths) }}
            </div>

            <div class="text-2xl mb-4">
                <span class="font-bold">Total:</span>
                {{ numberWithDots(stats.TotalDeaths) }}
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: 'DataBoxes',
    props: ['stats'],
    methods: {
        numberWithDots(x) {
            return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.')
        }
    }
}
</script>
