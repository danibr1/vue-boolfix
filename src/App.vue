<template>
    <div id="app">
        <Header @search="getData" />

        <!-- HOME-PAGE FILMS -->
        <section v-if="loadingSearch">
            <FilmsHomePage
                :discover="discoverList"
                :tradingTV="tradingTVList"
                :tradingMovies="tradingMoviesList"
            />
        </section>

        <!-- SEARCHED MOVIES -->
        <section v-else>
            <FilmsSearch :films="moviesList.concat(seriesList)" />
        </section>
    </div>
</template>

<script>
import axios from 'axios';

import Header from '@/components/Header.vue';
import FilmsHomePage from '@/components/FilmsHomePage.vue';
import FilmsSearch from '@/components/FilmsSearch.vue';

export default {
    name: 'App',
    components: {
        Header,
        FilmsSearch,
        FilmsHomePage,
    },
    data() {
        return {
            // Default
            apiKey: '486ea1d24aaf19cdf5b08c8d82fbf42d',

            // Search
            apiURL: 'https://api.themoviedb.org/3/search/',
            moviesList: [],
            seriesList: [],
            loadingSearch: true,

            // Home-Page
            discoverAPI: 'https://api.themoviedb.org/3/discover/movie',
            discoverList: [],

            trandingTVAPI: 'https://api.themoviedb.org/3/trending/tv/week',
            tradingTVList: [],
            trandingMoviesAPI:
                'https://api.themoviedb.org/3/trending/movies/week',
            tradingMoviesList: [],
        };
    },
    created() {
        // API DISCOVER
        axios
            .get(this.discoverAPI, {
                params: {
                    api_key: this.apiKey,
                    language: 'it-IT',
                },
            })
            .then((res) => {
                this.discoverList = res.data.results;
                this.loading = false;
            })
            .catch((err) => {
                console.log('Error', err);
            });

        // API TRADING TV
        axios
            .get(this.trandingTVAPI, {
                params: {
                    api_key: this.apiKey,
                    language: 'it-IT',
                },
            })
            .then((res) => {
                this.tradingTVList = res.data.results;
                this.loading = false;
            })
            .catch((err) => {
                console.log('Error', err);
            });

        // API TRADING MOVIES
        axios
            .get(this.trandingMoviesAPI, {
                params: {
                    api_key: this.apiKey,
                    language: 'it-IT',
                },
            })
            .then((res) => {
                this.tradingMoviesList = res.data.results;
                this.loading = false;
            })
            .catch((err) => {
                console.log('Error', err);
            });
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
                    this.loadingSearch = false;
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
                    this.loadingSearch = false;
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
