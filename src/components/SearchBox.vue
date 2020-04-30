<template>
    <div id="search-box">
        <input type="text" class="search-input"
               placeholder="Search"
               v-model="query"
               @keyup.enter="searchCity()"
        >
    </div>
</template>

<script>
    import { bus} from "../main";

    export default {
        name: "SearchBox",
        data() {
            return {
                query: ''
            }
        },
        methods: {
            searchCity() {
                bus.$emit('searchCity', this.query)
            }
        }
    }
</script>

<style scoped>
    #search-box {
        margin-bottom: 2rem;
    }

    .search-input {
        display: block;
        width: 100%;
        padding: 12px;
        transition: 0.5s;

        color: #172405;
        font-size: 1.2rem;

        border: none;
        outline: none;
        background: rgba(255, 255, 255, 0.4);
        border-radius: 20px;
        box-shadow: 0px 0px 5px 1px #dedede
    }

    .search-input:focus {
        background: #fff;
    }
</style>
