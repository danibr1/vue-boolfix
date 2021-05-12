<template>
    <div>
        <!-- CARD -->
        <ul>
            <!-- POSTER -->
            <li>
                <img v-if="info.poster_path != null"
                    :src="`https://image.tmdb.org/t/p/w342/${info.poster_path}`" 
                    :alt=" info.stitle == null ? info.name : info.title "
                >
                <!-- Poster = null -->
                <img v-else
                    :src="require('@/assets/img/poster-null.png')" alt=""
                >
            </li>
            <!-- NAME: Check movies or series -->
            <li>
                <strong>Titolo:</strong>  
                {{ info.title == null ? info.name : info.title }}
            </li>
            
            <!-- ORIGINAL NAME: check movies or series -->
            <li>
                <strong>Titolo originale:</strong> 
                <span>{{ info.original_title == null ? info.original_name : info.original_title }}</span>
            </li>
            
            <!-- LANGUAGE: Check if not include array language -->
            <li v-if="!flags.includes(info.original_language)">
                <strong>Lingua: </strong> 
                <span>{{info.original_language}}</span>
            </li>

            <!-- LANGUAGE FLAG IMG: if language = IT / EN -->
            <li class="flag-language flex" v-else>
                <strong>Lingua:</strong>
                <img 
                    class="flag-language"
                    :src="require(`@/assets/img/${info.original_language}.png`)" 
                    alt="info.original_language"
                >
            </li>
            
            <!-- VOTE -->
            <li>
                <strong>Voto:</strong> 
                <span>{{(info.vote_average / 2).toFixed(2) }}</span>
                <!-- Full stars -->
                <i
                    v-for="(star, index) in Math.floor(info.vote_average / 2)"
                    :key="'fullStar'+index"
                    class="fas fa-star"
                >
                </i>
                <!-- Half stars -->
                <i
                    v-show="((info.vote_average / 2) - Math.floor(info.vote_average / 2) > 0.49)"
                    class="fas fa-star-half-alt"
                >
                </i>
                <!-- Empty stars with precedent half star-->
                <span v-if="((info.vote_average / 2) - Math.floor(info.vote_average / 2) > 0.49)"
                >
                    <i	
                        v-for="(star, index) in 4 - Math.floor(info.vote_average / 2)"
                        :key="'emptyStar'+index"
                        class="far fa-star"
                    >
                    </i>
                </span>
                <!-- Empty stars without half star-->
                <span v-else>
                    <i	
                        v-for="(star, index) in 5 - Math.floor(info.vote_average / 2)"
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
    props: {
        info: Object,
    },
    data () {
        return {
            flags: ["it", "en", "de", "es", "pt", "hi", "fr", "cs", "hu", "ko", "nl", "ja"],
        };
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