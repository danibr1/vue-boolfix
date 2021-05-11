<template>
    <div id="app">
	
		<Header @search="searchFilm"/>

		<!-- Merge result array in "films" -->
		<Main :films="moviesList.concat(seriesList)"/>

	</div>
</template>

<script>
import axios from 'axios';

import Header from './components/Header.vue';
import Main from './components/Main.vue';

export default {
    name: 'App',
    components: {
        Header,
		Main,
    },
	data() {
		return {
			moviesList: [],
			seriesList: [],
			movieDefaultUrl: "https://api.themoviedb.org/3/movie/550?api_key=486ea1d24aaf19cdf5b08c8d82fbf42d",
			seriesDefaultUrl: "https://api.themoviedb.org/3/tv/550?api_key=486ea1d24aaf19cdf5b08c8d82fbf42d",
		}
	},
	methods: {
		// API CALL MOVIES
		searchFilm(search) {
			axios
				.get ("https://api.themoviedb.org/3/search/movie?api_key=486ea1d24aaf19cdf5b08c8d82fbf42d", {
					params: {
						query: search,
						language: "it-IT"
					},
				})
				.then((res) => {
					this.moviesList = res.data.results;
				})
				.catch((err) => {
					console.log('Error', err);
				});
			
			// API CALL SERIES
			axios
				.get ("https://api.themoviedb.org/3/search/tv?api_key=486ea1d24aaf19cdf5b08c8d82fbf42d", {
					params: {
						query: search,
						language: "it-IT"
					},
				})
				.then((res) => {
					this.seriesList = res.data.results;
				})
				.catch((err) => {
					console.log('Error', err);
				});
			},
		},
	};
</script>


<style lang="scss">
	// SCSS GENERAL

</style>
