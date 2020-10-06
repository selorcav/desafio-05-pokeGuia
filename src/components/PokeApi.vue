<template>
    <div>
        <h1>PokeGuía</h1>
        <p>Nombre</p>
        <input v-model="pokemonName" @keyup.enter="searchPokemon" type="text">
        <button @click="searchPokemon">Buscar</button>
        <br>
        <img v-if="currentPokemon.sprites" :src="currentPokemon.sprites.front_default" alt="">
        <h2>Moves</h2>
        <ul>
            <li v-for="move in currentPokemon.moves" :key="move.name">
                {{move.move.name}} 
            </li>
        </ul>
        <h2>Abilities</h2>
        <ul>
            <li v-for="ability in currentPokemon.abilities" :key="ability.name">
                {{ability.ability.name}}
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    data() {
        return {
            currentPokemon: {},
            pokemonName: "pikachu"
        }
    },
    created() {
        fetch(`https://pokeapi.co/api/v2/pokemon/${this.lower}`) 
        .then(data => data.json())
        .then(response => this.currentPokemon = response)
    },
    methods: {
        searchPokemon(){
            fetch(`https://pokeapi.co/api/v2/pokemon/${this.lower}`)  
            .then(data => data.json())
            .then(response => this.currentPokemon = response)
        }
    },
    computed: {
        moves(){
            return this.currentPokemon.moves
        },
        abilities(){
            return this.currentPokemon.abilities
        },
        lower(){
            return this.pokemonName.toLowerCase()
        }
    },
    
    
}
</script>

<style>
ul{
    list-style: none;
}
</style>