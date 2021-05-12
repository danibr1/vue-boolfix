<template>
    <div>
        <!-- CARD -->
        <ul>
            <!-- POSTER -->
            <li>
                <img v-if="details.poster_path != null"
                    :src="`https://image.tmdb.org/t/p/w342/${detailsposter_path}`" 
                    :alt=" details.stitle == null ? details.name : details.title "
                >
                <!-- Poster = null -->
                <img v-else
                    :src="require('@/assets/img/poster-null.png')" alt=""
                >
            </li>
            <!-- NAME: Check movies or series -->
            <li>
                <strong>Titolo:</strong>  
                {{ details.title == null ? details.name : details.title }}
            </li>
            
            <!-- ORIGINAL NAME: check movies or series -->
            <li>
                <strong>Titolo originale:</strong> 
                <span>{{ details.original_title == null ? details.original_name : details.original_title }}</span>
            </li>
            
            <!-- LANGUAGE: Check if not include array language -->
            <li v-if="!flags.includes(details.original_language)">
                <strong>Lingua: </strong> 
                <span>{{details.original_language}}</span>
            </li>

            <!-- LANGUAGE FLAG IMG: if language = IT / EN -->
            <li class="flag-language flex" v-else>
                <strong>Lingua:</strong>
                <img 
                    class="flag-language"
                    :src="require(`@/assets/img/${details.original_language}.png`)" 
                    alt="details.original_language"
                >
            </li>
            
            <!-- VOTE -->
            <li>
                <strong>Voto:</strong> 
                <span>{{(details.vote_average / 2).toFixed(2) }}</span>
                <!-- Full stars -->
                <i
                    v-for="(star, index) in Math.floor(details.vote_average / 2)"
                    :key="'fullStar'+index"
                    class="fas fa-star"
                >
                </i>
                <!-- Half stars -->
                <i
                    v-show="((details.vote_average / 2) - Math.floor(details.vote_average / 2) > 0.49)"
                    class="fas fa-star-half-alt"
                >
                </i>
                <!-- Empty stars with precedent half star-->
                <span v-if="((details.vote_average / 2) - Math.floor(details.vote_average / 2) > 0.49)"
                >
                    <i	
                        v-for="(star, index) in 4 - Math.floor(details.vote_average / 2)"
                        :key="'emptyStar'+index"
                        class="far fa-star"
                    >
                    </i>
                </span>
                <!-- Empty stars without half star-->
                <span v-else>
                    <i	
                        v-for="(star, index) in 5 - Math.floor(details.vote_average / 2)"
                        :key="'emptyStar'+index"
                        class="far fa-star"
                    >
                    </i>
                </span>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name: 'Card',
    props:  {
        datails: Object,
    },
    data () {
        return {
            flags: ["it", "en", "de", "es", "pt", "hi", "fr", "cs", "hu", "ko", "nl", "ja"],
        }
    }
}
</script>

<style>

</style>