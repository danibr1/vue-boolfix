<template> 
	<main>
		<section class="movies">
			<h1>Movie</h1>

			<ul class="movie-list">
				<li v-for="item in movies" :key="item.id">
					<div>{{ item.title }}</div>
					<div>{{ item.original_title }}</div>
					<div>{{ item.original_language }}</div>
					<div>{{ item.vote_average }}</div>
				</li>
			</ul>
		</section>

	</main>
</template>

<script>
export default {
	name: 'Main',
	props: {
		movies: Array,
	}
}
</script>

<style scoped lang="scss">
	li {
		margin-bottom: 1rem;
	}
</style>
