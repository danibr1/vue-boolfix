<template>
    <header class="flex jc-between ai-center "> 
		<!-- BRAND -->
        <img :src='logo.img' :alt="logo.name">
        
        <!-- SEARCH -->
        <Search @search="searchItem"/>
      
	</header>
</template>

<script>
import Search from '@/components/Search.vue';

export default {
    name: 'Header',
    components: {
        Search,    
    },
    data (){
        return {
            searchFilm: '',
            logo: {
                img: require('@/img/bruno.png'),
                name: 'Brunoflix'
            },
        }
    },
    methods: {
        searchItem(text) {
            this.searchFilm = text;
            this.$emit('search', this.searchFilm)
        }
    }
};
</script>

<style scoped lang="scss">
@import '@/styles/general';
  
    img {
        width: 150px;
    }

</style>
