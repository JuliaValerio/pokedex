<template>
    <section class="pokemons-container">
        <input placeholder="Search" name="search" id="search" type="text" v-model="search">
        <!-- {{pokemons}} -->
        <div class="pokemons" v-if="search.length == 0">
            <div class="pokemon" v-for="pokemon in pokemons" :key="pokemon.id">
                <img :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${pokemon.url.split(`/`)[6]}.png`" :alt="pokemon.name"/>
                <span>
                    <p class="title">{{pokemon.name}}</p>
                    <p>#{{pokemon.url.split("/")[6]}}</p>
                </span>
            </div>
        </div>
        <div class="pokemons" v-else>
            <div class="pokemon" v-for="pokemon in filtered_pokemons" :key="pokemon.id">
                <img :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${pokemon.url.split(`/`)[6]}.png`" :alt="pokemon.name"/>
                <span>
                    <p class="title">{{pokemon.name}}</p>
                    <p>#{{pokemon.url.split("/")[6]}}</p>
                </span>
            </div>
        </div>
    </section>
</template>

<script>
import { api } from "@/services.js";

export default {
    name: "TheList",
    data() {
        return {
            pokemons: null,
            search: "",
        }
    },
    computed: {
        filtered_pokemons() {
            return this.pokemons.filter((item) => {
                return item.name.includes(this.search);
            });
        },
    },
    methods: {
        getPokemons () {
            api.get("/pokemon?limit=151").then(response => {
                this.pokemons = response.data.results;
                console.log(response.data.results)
            });
        }
    },
    created() {
        this.getPokemons();
    }
};
</script>

<style scoped>
    .pokemons-container{
        max-width: 100em;
        margin: 0 auto;
        text-align: center;
    }
    .pokemons{
        display: grid;
        grid-template-columns: repeat(6, 1fr);
        grid-gap: 1em;
        margin: 1em;
    }
    .pokemon{
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-between;
        box-shadow: 0 4px 8px rgba(30,60,90, 0.1);
        border-radius: .3em;
        background: #FFF;
        transition: all .2s;
        padding: 1em;
    }
    .pokemon img{
        width: 10em;
    }
    .pokemon span{
        width: 100%;
        display: flex;
        justify-content: space-between;
    }
    .pokemon:hover{
        box-shadow: 0 4px 8px rgba(30,60,90, 0.2);
        transform: scale(1.1);
        position: relative;
        z-index: 1;
    }
    input{
        flex: 1 1 auto;
        line-height: 20px;
        padding: 10px;
        width: 97%;
        border: none;
        border-bottom: solid 1px;
        margin-top: 2em;
        margin-bottom: 2em;
        box-shadow: 0 4px 8px rgba(30,60,90, 0.2);
    }
    input::placeholder{
        padding: 1px 20px;
    }
</style>
