<template> 
    <!-- FORM SEARCH FILM -->
    <form>
        <input 
            v-model="searchFilm"
            type="text"
            name="search"
            id="search"
            placeholder="Search Film"
        >
        <button
            class="btn"
            type="submit"
            @click.prevent="$emit('search', searchFilm)"
        >
        Cerca
        </button>
      
    </form>
</template>

<script>
export default {
    name: 'Search',
    data () {
        return {
            searchFilm:'',
        }
    }
};
</script>

<style scoped lang="scss">

</style>