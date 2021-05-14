<template>
    <!-- FORM SEARCH FILM -->
    <form>
        <ul class="flex jc-center ai-center">
            <li>
                <a href="#" v-if="searchFilm != ''">
                    <i class="fas fa-times" @click="resetInput"></i>
                </a>
            </li>
            <li>
                <input
                    v-model.trim="searchFilm"
                    type="text"
                    name="search"
                    id="search"
                    placeholder="Cerca movies, serie TV"
                    @keyup="$emit('search', searchFilm)"
                />
            </li>
            <li>
                <button
                    class="btn"
                    type="submit"
                    @click.prevent="$emit('search', searchFilm)"
                >
                    <i class="fas fa-search"></i>
                </button>
            </li>
            <li>
                <a href="#"><i class="fas fa-bell"></i></a>
            </li>
            <li>
                <a href="#"
                    ><img
                        class="profile-icon"
                        src="https://i.pinimg.com/564x/b4/0f/9f/b40f9f8fc0fb88aabf2a8acbc39c0ac0.jpg"
                        alt=""
                /></a>
            </li>
        </ul>
    </form>
</template>

<script>
export default {
    name: 'Search',
    data() {
        return {
            searchFilm: '',
            submited: '',
        };
    },
    methods: {
        resetInput() {
            this.searchFilm = '';
            this.$emit('search', this.searchFilm);
        },
    },
};
</script>

<style scoped lang="scss">
@import '@/styles/general';

input {
    width: 280px;
    height: 2.5rem;
    color: #fff;
    border: 2px solid #fff;
    background: #000;
    padding: 5px 10px;
    &:hover,
    &:focus {
        background: rgb(51, 51, 51);
    }
}

.btn {
    background: none;
    border: none;
    color: #fff;
    font-size: 1rem;
    cursor: pointer;
}

li {
    margin-right: 30px;
    &:first-child {
        margin-right: 10px;
    }
    &:nth-child(2) {
        margin-right: 10px;
    }
    i {
        font-size: 1.3rem;
        transition: color 0.3s;
        &:hover {
            color: rgb(172, 170, 170);
        }
    }
    img {
        width: 35px;
        border-radius: 3px;
    }
}
</style>
