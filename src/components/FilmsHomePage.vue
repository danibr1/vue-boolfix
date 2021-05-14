<template>
    <main>
        <!-- NEW FILMS -->
        <section>
            <h2>Scopri i nuovi film</h2>
            <vueCustomScrollbar class="cards">
                <div class="flex ai-center">
                    <Card
                        v-for="item in discover"
                        :key="item.id"
                        :info="item"
                    />
                </div>
            </vueCustomScrollbar>
        </section>

        <!-- SERIES OF THE WEEK -->
        <section>
            <h2>Le serie TV della settimana</h2>
            <vueCustomScrollbar class="cards">
                <div class="flex ai-center">
                    <Card
                        v-for="item in tradingTV"
                        :key="item.id"
                        :info="item"
                    />
                </div>
            </vueCustomScrollbar>
        </section>

        <!-- MOVIES OF THE WEEK -->
        <section>
            <h2>I film della settimana</h2>
            <vueCustomScrollbar class="cards">
                <div class="flex ai-center">
                    <Card
                        v-for="item in tradingMovies"
                        :key="item.id"
                        :info="item"
                    />
                </div>
            </vueCustomScrollbar>
        </section>
    </main>
</template>

<script>
import vueCustomScrollbar from 'vue-custom-scrollbar';
import 'vue-custom-scrollbar/dist/vueScrollbar.css';
import Card from '@/components/Card';

export default {
    name: 'FilmsHomePage',
    components: {
        Card,
        vueCustomScrollbar,
    },
    props: {
        discover: Array,
        tradingMovies: Array,
        tradingTV: Array,
    },
};
</script>

<style scoped lang="scss">
@import '@/styles/general';
section {
    margin-bottom: 50px;
}
main {
    padding: 0 60px;
    h2 {
        margin: 1rem 0;
    }
}
.cards {
    height: 570px;
    overflow-x: scroll;
    padding: 20px 10px;
}
</style>
