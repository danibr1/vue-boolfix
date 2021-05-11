<template> 
	<main>
		<section class="movies">
			<h1>Movies</h1>

			<ul class="movie-list">
				<li v-for="item in films" :key="item.id">
					
					<ul>
						<!-- POSTER -->
						<li>
							<img v-if="item.poster_path != null"
								:src="`https://image.tmdb.org/t/p/w342/${item.poster_path}`" alt="item."
							>
							<!-- Poster = null -->
							<img v-else
								:src="require('@/assets/img/poster-null.png')" alt=""
							>

						</li>
						<!-- NAME: Check movies or series -->
						<li>
							<strong>Titolo:</strong>  
							{{ item.title == null ? item.name : item.title }}
						</li>
						
						<!-- ORIGINAL NAME: check movies or series -->
						<li>
							<strong>Titolo originale:</strong> 
							<span>{{ item.original_title == null ? item.original_name : item.original_title }}</span>
						</li>
						
						<!-- LANGUAGE: Check if not include "it" & "en" -->
						<li v-if="!flags.includes(item.original_language)">
							<strong>Lingua: </strong> 
							<span>{{item.original_language}}</span>
						</li>

						<!-- LANGUAGE FLAG IMG: if language = IT / EN -->
						<li class="flag-language flex" v-else>
							<strong>Lingua</strong>
							<img 
								class="flag-language"
								:src="require(`@/assets/img/${item.original_language}.png`)" 
								alt="item.original_language"
							>
						</li>
						
						<!-- VOTE -->
						<li>
							<strong>Voto:</strong> 
							<span>{{item.vote_average}}</span>
						</li>

					</ul>

				</li>
			</ul>
		</section>

	</main>
</template>

<script>
export default {
	name: 'Main',
	props: {
		films: Array,
	},
	data () {
		return {
			flags: ["it", "en"],
		};
	}
}
</script>

<style scoped lang="scss">
@import '@/styles/general';
	ul {
		margin: 1rem 0;
		li {
			margin-bottom: 2px;
			}
	}

	.flag-language {
		width: 30px;
		height: 14px;
	}
</style>
