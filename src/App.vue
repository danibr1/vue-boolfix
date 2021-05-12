<template>
    <div id="app">
	
		<Header @search="getData"/>

		<div v-if="!loading && result===true">
			<!-- Merge result array in "films" -->
			<Main :films="moviesList.concat(seriesList)"/>
		</div>
		<div v-else>Nessun risultato > effettua una ricerca</div>

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
			apiURL: 'https://api.themoviedb.org/3/search/',
			apiKey: '486ea1d24aaf19cdf5b08c8d82fbf42d',
			moviesList: [],
			seriesList: [],
			movieDefaultUrl: "https://api.themoviedb.org/3/movie/550?api_key=486ea1d24aaf19cdf5b08c8d82fbf42d",
			seriesDefaultUrl: "https://api.themoviedb.org/3/tv/550?api_key=486ea1d24aaf19cdf5b08c8d82fbf42d",
			loading: true,
			result: false,
		}
	},
	methods: {
		// API CALL MOVIES

		


		getData(searchText) {
			axios
				.get (this.apiURL + 'movie', {
					params: {
						api_key: this.apiKey,
						query: searchText,
						language: "it-IT"
					},
				})
				.then((res) => {
					this.moviesList = res.data.results;
					this.loading = false;
					this.result = true;
				})
				.catch((err) => {
					console.log('Error', err);
				});
			
			// API CALL SERIES
			axios
				.get (this.apiURL + 'tv', {
					params: {
						api_key: this.apiKey,
						query: searchText,
						language: "it-IT"
					},
				})
				.then((res) => {
					this.seriesList = res.data.results;
					this.loading = false;
					this.result = true;
				})
				.catch((err) => {
					console.log('Error', err);
				});
			},
		},
	};
</script>


<style lang="scss">

</style>
