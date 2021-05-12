<template>
    <header class="flex jc-between ai-center "> 
        <!-- BRAND -->
        <img :src="logo.img" :alt="logo.name">
        
        <!-- SEARCH -->
        <Search @search="getData"/>
	</header>
</template>

<script>
import Search from '@/components/Search';

export default {
    name: 'Header',
    components: {
        Search,    
    },
    data (){
        return {
            searchText: '',
            logo: {
                img: "https://fontmeme.com/permalink/210511/ba5cfce3f8e07f7651ec5e9120c84736.png",
                name: 'Brunoflix'
            },
        }
    },
    methods: {
        getData(text) {
            this.searchText = text;
            this.$emit('search', this.searchText)
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