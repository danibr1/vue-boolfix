<template>
    <header>
        <div class="flex jc-between jc-center ai-center">
            <!-- BRAND -->
            <div class="flex jc-center ai-center">
                <a href="#"><img :src="logo.img" :alt="logo.name"/></a>

                <ul class="flex">
                    <li>Home</li>
                    <li>Serie Tv</li>
                    <li>Film</li>
                    <li>Nuovi e popolari</li>
                    <li>La mia lista</li>
                </ul>
            </div>

            <!-- SEARCH -->
            <Search @search="getData" />
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
    data() {
        return {
            searchText: '',
            logo: {
                img:
                    'https://fontmeme.com/permalink/210511/ba5cfce3f8e07f7651ec5e9120c84736.png',
                name: 'Brunoflix',
            },
        };
    },
    methods: {
        getData(text) {
            this.searchText = text;
            this.$emit('search', this.searchText);
        },
    },
};
</script>

<style scoped lang="scss">
@import '@/styles/general';

header {
    background: $bg-header;
    color: $text-white;
    padding: 25px 60px;
    img {
        margin-right: 30px;
        width: 140px;
    }
    li {
        font-size: 1rem;
        margin-right: 20px;
        cursor: pointer;
        transition: color 0.3s;
        &:first-child {
            font-weight: bold;
        }
        &:last-child {
            margin-right: 0px;
        }
        &:hover {
            color: rgb(172, 170, 170);
        }
    }
}
</style>
