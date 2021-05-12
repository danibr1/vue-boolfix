<template> 
	<main>
		<section class="movies">
			<h1>Movies</h1>

			<div>
				<!-- Elemento CARD -->
				<Card v-for="item in films" :key="item.id" :datails="item"/>
			</div>

		</section>
	</main>
</template>

<script>
import Card from '@/components/Card';

export default {
	name: 'Main',
	components: {
		Card,
	},
	props: {
		films: Array,
	},
}
</script>

<style scoped lang="scss">
@import "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css";
@import '@/styles/general';

	ul {
		margin: 1rem 0;
		li {
			margin-bottom: 2px;
			}
	}

	.flag-language {
		width: 60px;
		height: 24px;
	}
</style>