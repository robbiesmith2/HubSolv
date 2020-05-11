<template>
    <div class="ratings">
        <img v-bind:src="findIcon(icon)" class="ratings__icon" /><span>{{ rating }}</span>
    </div>
</template>

<script>
import imdb from '../assets/IMDB.svg';
import rottentomatoes from '../assets/tomatometer.svg';
import metacritic from '../assets/Metacritic.svg';

export default {
    name: 'rating',
    props: [ 'rating', 'icon' ],
    data() {
        return {
            imdb: imdb,
            rottentomatoes: rottentomatoes,
            metacritic: metacritic
        }
    },
    methods: {
        // use this function to dynamically render the correct icon
        findIcon(source) {
            if (source === "Internet Movie Database") {
                return this.imdb;
            } else if (source === "Rotten Tomatoes") {
                return this.rottentomatoes
            } else {
                return this.metacritic
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