<template> 
	<main class="container">
		
		<section class="cards">
			<h1>Movies</h1>
			<div class="flex">
				<Card v-for="item in films" :key="item.id" :info="item"/>
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

.cards {
	widows: 100%;
	overflow-x: auto
}


</style>