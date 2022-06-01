<template>
    <section class="pokemons-container">
        <!-- {{pokemons}} -->
        <div class="pokemons">
            <div class="pokemon" v-for="pokemon in pokemons" :key="pokemon.id">
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
export default {
    name: "TheList",
    data() {
        return {
            pokemons: null
        }
    },
    methods: {
        getPokemons () {
            fetch("https://pokeapi.co/api/v2/pokemon?limit=151")
            .then(response => response.json())
            .then(response => {
                this.pokemons = response.results
                console.log(response.results)
            })
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
</style>
