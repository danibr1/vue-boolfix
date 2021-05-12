<template> 
	<main>
		<section class="movies">
			<h1>Movies</h1>

			<div v-for="item in films" :key="item.id">
				<Card :info="item"/>
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

</style>