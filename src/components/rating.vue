<template>
    <div class="ratings">
        <img v-bind:src="findIcon(icon)" class="ratings__icon" /><span>{{ rating }}</span>
    </div>
</template>

<script>
export default {
    name: 'rating',
    props: [ 'rating', 'icon' ],
    methods: {
        // use this function to dynamically render the correct icon
        findIcon(source) {
            if (source === "Internet Movie Database") {
                return 'IMDB.svg'
            } else if (source === "Rotten Tomatoes") {
                return 'tomatometer.svg'
            } else {
                return 'Metacritic.svg'
            }
        }
    }
}
</script>

<style lang="scss" scoped>
    .ratings {
        display: flex;
        align-items: center;
        margin-right: 2rem;

        &__icon {
            max-width: 60px;
            max-height: 20px;
            margin-right: 0.5rem;
        }
    }
</style>