<template>
    <div id="app">
        <Header @search="getData" />

        <div v-if="!loading">
            <!-- Merge result array in "films" -->
            <Main :films="moviesList.concat(seriesList)" />
        </div>
        <div class="loading" v-else>
            Nessun risultato > effettua una ricerca
        </div>
    </div>
</template>

<script>
import axios from 'axios';

import Header from '@/components/Header.vue';
import Main from '@/components/Main.vue';

export default {
    name: 'App',
    components: {
        Header,
        Main,
    },
    data() {
        return {
            apiURL: 'https://api.themoviedb.org/3/search/',

            trandingMoviesAPI:
                'https://api.themoviedb.org/3/trending/movies/week',
            // trandingTVAPI: "https://api.themoviedb.org/3/trending/tv/week",
            // discoverAPI: "https://api.themoviedb.org/3/discover/movie",

            apiKey: '486ea1d24aaf19cdf5b08c8d82fbf42d',
            moviesList: [],
            seriesList: [],
            loading: true,
            result: false,
        };
    },
    methods: {
        // API CALL MOVIES
        getData(searchText) {
            axios
                .get(this.apiURL + 'movie', {
                    params: {
                        api_key: this.apiKey,
                        query: searchText,
                        language: 'it-IT',
                    },
                })
                .then((res) => {
                    this.moviesList = res.data.results;
                    this.loading = false;
                })
                .catch((err) => {
                    console.log('Error', err);
                });

            // API CALL SERIES
            axios
                .get(this.apiURL + 'tv', {
                    params: {
                        api_key: this.apiKey,
                        query: searchText,
                        language: 'it-IT',
                    },
                })
                .then((res) => {
                    this.seriesList = res.data.results;
                    this.loading = false;
                })
                .catch((err) => {
                    console.log('Error', err);
                });
        },
    },
};
</script>

<style lang="scss">
@import '@/styles/general';

#app {
    min-width: 100vh;
    min-height: 100vh;
    color: $text-white;
    background: $bg-app;
    .loading {
        padding: 25px 60px;
    }
}
</style>
