<template>
    <article class="results__result">
        <p v-if="loading">Loading</p>
        <div v-if="isLoaded" class = "movie-detail">
            <h2 class="movie-detail__title">{{ movieDetails.Title }} <span>({{ movieDetails.Year }})</span></h2>
            <div class="movie-detail__meta">
                <span>{{ movieDetails.Genre }}</span>
                <span>{{ movieDetails.Language }}</span>
                <span>{{ movieDetails.Runtime }}</span>
            </div>
            <div v-if="movieDetails.Rated != 'N/A'" class="movie-details__rated">
                {{ movieDetails.Rated }}
            </div>
            <div class="movie-detail__ratings">
                <rating
                v-for="rating in movieDetails.Ratings"
                :key="rating.Source"
                v-bind:rating="rating.Value"
                v-bind:icon="rating.Source" />
            </div>
            <div v-if="movieDetails.Plot && movieDetails.Plot != 'N/A'" class="movie-detail__plot">
                <h3>Overview:</h3>
                <p>{{ movieDetails.Plot }}</p>
                <p>Directed by {{ movieDetails.Director }}</p>
            </div>
            <div v-if="movieDetails.Actors && movieDetails.Actors != 'N/A'" class="movie-detail__cast">
                <h3>Starring:</h3>
                <p>{{ movieDetails.Actors }}</p>
            </div>
            <img v-if="movieDetails.Poster && movieDetails.Poster != 'N/A'" class="movie-detail__image" v-bind:src="movieDetails.Poster" />
            <div v-if="!movieDetails.Poster || movieDetails.Poster === 'N/A'" class="movie-detail__image movie-detail__image--fallback">
                <p><span>Sorry</span>No image found</p>
            </div>
        </div>
    </article>
</template>

<script>
    import rating from './rating.vue';

    export default {
        name: 'movieResult',
        components: { rating },
        props: [ 'movie' ],
        data() {
            return {
                movieDetails: {},
                isLoaded: false,
                loading: false
            }
        },
        mounted() {
            this.fetchMovieData()
        },
        methods: {
            // fetch data to show movie details 
            fetchMovieData() {
                // update loading states
                this.isLoaded = false;
                this.loading = true;
                fetch(`https://movie-database-imdb-alternative.p.rapidapi.com/?i=${this.movie.imdbID}&type=movie&r=json&plot=full`, {
                    "method": "GET",
                    "headers": {
                        "x-rapidapi-host": "movie-database-imdb-alternative.p.rapidapi.com",
                        "x-rapidapi-key": "87cd541c16msh01a954c6070da2fp1d5a57jsn4f43f3512649"
                    }
                })
                .then(res => {
                    return res.json();
                })
                .then(this.setMovieDetails, this.loading = false)
                .catch(err => {
                    console.log(err);
                })
            },
            setMovieDetails(results) {
                // store the results and set the loaded state to true
                this.movieDetails = results
                this.isLoaded = true
            }
        }
    }
</script>