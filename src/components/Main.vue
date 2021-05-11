<template> 
	<main>
		<section class="movies">
			<h1>Movies</h1>

			<ul class="movie-list">
				<li v-for="item in films" :key="item.id">
					
					<ul>
						<!-- Check Name movies or series -->
						<li>
							<strong>Titolo:</strong>  
							{{ item.title == null ? item.name : item.title }}
						</li>
						
						<!-- Check Original Name movies or series -->
						<li>
							<strong>Titolo originale:</strong> 
							{{ item.original_title == null ? item.original_name : item.original_title }}
						</li>
						
						
						<li v-if="!flags.includes(item.original_language)">
							<strong>Lingua: </strong> {{item.original_language}}
						</li>

						<!-- FLAG IF LANGUAGE = IT / EN -->
						<li class="flag-language flex" v-else>
							<strong>Lingua</strong>
							<img 
								class="flag-language"
								:src="require(`@/assets/img/${item.original_language}.png`)" 
								alt="item.original_language"
							>
						</li>
						
						<li><strong>Voto:</strong> {{item.vote_average}}</li>

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
