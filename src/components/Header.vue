<template>
    <header> 
        
        <div class="container flex jc-between jc-center ai-center">
            <!-- BRAND -->
            <img :src="logo.img" :alt="logo.name">
            
            <!-- SEARCH -->
            <Search @search="getData"/>
        </div>
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
    
    header {
        background: $bg-header;
        padding: 10px;
    }

    img {
        width: 150px;
    }

</style>