<template>
    <main>
        <h2>Movies - Risultati della ricerca</h2>
        <vueCustomScrollbar class="cards">
            <div class="flex ai-center">
                <Card v-for="item in films" :key="item.id" :info="item" />
            </div>
        </vueCustomScrollbar>
    </main>
</template>

<script>
import vueCustomScrollbar from 'vue-custom-scrollbar';
import 'vue-custom-scrollbar/dist/vueScrollbar.css';
import Card from '@/components/Card';

export default {
    name: 'FilmsSearch',
    components: {
        Card,
        vueCustomScrollbar,
    },
    props: {
        films: Array,
    },
    computed: {},
};
</script>

<style scoped lang="scss">
@import '@/styles/general';

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
