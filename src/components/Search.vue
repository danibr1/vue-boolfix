<template>
    <!-- FORM SEARCH FILM -->
    <form class="flex jc-center ai-center">
        <input
            v-model.trim="searchFilm"
            type="text"
            name="search"
            id="search"
            placeholder="Titoli, persone, generi"
        />
        <span>
            <button
                class="btn"
                type="submit"
                @click.prevent="$emit('search', searchFilm)"
                @click="resetInput"
            >
                <i class="fas fa-search"></i>
            </button>
        </span>
        <span>
            <a href="#"><i class="fas fa-bell"></i></a>
        </span>
        <span>
            <a href="#"
                ><img
                    class="profile-icon"
                    src="https://i.pinimg.com/564x/b4/0f/9f/b40f9f8fc0fb88aabf2a8acbc39c0ac0.jpg"
                    alt=""
            /></a>
        </span>
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
        },
    },
};
</script>

<style scoped lang="scss">
@import '@/styles/general';

input {
    width: 200px;
    height: 1.8rem;
    color: #fff;
    border: 2px solid #fff;
    background: #000;
    padding: 5px 10px;
    margin-right: 10px;
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

span {
    margin-right: 30px;
    &:first-child {
        margin-right: 5px;
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
