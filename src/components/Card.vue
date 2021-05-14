<template>
    <div class="card">
        <!-- FILM POSTER -->
        <img
            Class="poster"
            v-if="info.poster_path != null"
            :src="`https://image.tmdb.org/t/p/w342/${info.poster_path}`"
            :alt="info.stitle == null ? info.name : info.title"
        />
        <!-- Poster = null -->
        <img v-else :src="require('@/assets/img/poster-null.png')" alt="" />
        <!-- DETAILS    -->
        <ul>
            <!-- NAME: Check movies or series -->
            <li>
                <span class="strong">Titolo:</span>
                {{ info.title == null ? info.name : info.title }}
            </li>

            <!-- ORIGINAL NAME: check movies or series -->
            <li>
                <span class="strong">Titolo originale:</span>
                <span>{{
                    info.original_title == null
                        ? info.original_name
                        : info.original_title
                }}</span>
            </li>

            <!-- LANGUAGE: -->
            <li class="flex">
                <span class="strong">Lingua:</span>
                <img
                    class="flag-language"
                    v-if="isFlag(info.original_language)"
                    :src="require(`@/assets/img/${info.original_language}.png`)"
                    :alt="info.original_language"
                />
                <span v-else>{{ info.original_language }}</span>
            </li>

            <!-- VOTE -->
            <li>
                <span class="strong">Voto:</span>
                <span class="vote">{{
                    getStarVote(info.vote_average).toFixed(2)
                }}</span>
                <!-- Full stars -->
                <i
                    v-for="(star, index) in Math.floor(info.vote_average / 2)"
                    :key="'fullStar' + index"
                    class="fas fa-star"
                >
                </i>
                <!-- Half stars -->
                <i
                    v-show="
                        info.vote_average / 2 -
                            Math.floor(info.vote_average / 2) >
                            0.49
                    "
                    class="fas fa-star-half-alt"
                >
                </i>
                <!-- Empty stars with precedent half star-->
                <span
                    v-if="
                        info.vote_average / 2 -
                            Math.floor(info.vote_average / 2) >
                            0.49
                    "
                >
                    <i
                        v-for="(star, index) in 4 -
                            Math.floor(info.vote_average / 2)"
                        :key="'emptyStar' + index"
                        class="far fa-star"
                    >
                    </i>
                </span>
                <!-- Empty stars without half star-->
                <span v-else>
                    <i
                        v-for="(star, index) in 5 -
                            Math.floor(info.vote_average / 2)"
                        :key="'emptyStar' + index"
                        class="far fa-star"
                    >
                    </i>
                </span>
            </li>
            <li>
                <span class="strong">Descrizione:</span>
                <p class="overview">{{ info.overview }}</p>
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
    data() {
        return {
            flags: [
                'it',
                'en',
                'de',
                'es',
                'pt',
                'hi',
                'fr',
                'cs',
                'hu',
                'ko',
                'nl',
                'ja',
            ],
        };
    },
    methods: {
        isFlag(lang) {
            return this.flags.includes(lang);
        },
        getStarVote(vote) {
            return vote / 2;
        },
    },
};
</script>

<style scoped lang="scss">
@import '@/styles/general';

.card {
    position: relative;
    width: 342px;
    height: 513px;
    margin-right: 5px;
    overflow: hidden;
    cursor: pointer;
    border-radius: 5px;
    flex-shrink: 0;
    transition: all 0.2s ease-in-out;
    font-size: 16px;
    .poster {
        position: absolute;
        top: 0;
        left: 0;
        height: 100%;
        width: 100%;
    }
    &:hover {
        transform: scale(1.09);
        z-index: 1;
    }
}

.strong {
    font-weight: bold;
    margin-right: 5px;
}
.vote {
    margin-right: 5px;
}

ul {
    position: absolute;
    z-index: 1;
    top: 50%;
    transform: translateY(-50%);
    padding: 10px;
    left: 10px;
    opacity: 0;
    transition: opacity 0.3s;
    li {
        margin-bottom: 1rem;
        i {
            color: rgb(233, 200, 55);
        }
    }
}

.flag-language {
    width: 30px;
    height: 24px;
}

.overview {
    margin-top: 1rem;
    height: 250px;
    overflow: auto;
}

// LAYOVER
.card::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.8);
    transition: opacity 0.3s;
    opacity: 0;
}

.card:hover::after,
.card:hover ul {
    opacity: 1;
}
</style>
