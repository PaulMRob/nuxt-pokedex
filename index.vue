<template>
    
    <div class="card">
        <span class="card--id">#{{pokemon.id}}</span>
        <img class="card--image" src={{pokemon.image}} alt={{pokemon.name}} />
        <h1 class="card--name">{{pokemon.name}}</h1>
        <span class="card--details">{{pokemon.type}}</span>
    </div>

</template>

<script setup lang="ts">

const pokemons: number = 100

// Define pokemon interface
interface IPokemon {
    id: number;
    name: string;
    image: string;
    type: string;
}

// fetch and map over API Response data
const fetchData = (): void => {
    for (let i = 1; i <= pokemons; i++) {
        getPokemon(i)
    }
};

const getPokemon = async (id: number): Promise<void> => {
    const data: Response = await fetch(`https://pokeapi.co/api/v2/pokemon/${id}`)
    const pokemon: any = await data.json()
    const pokemonType: string = pokemon.types
        .map((poke: any) => poke.type.name)
        .join(", ")

    const transformedPokemon = {
        id: pokemon.id,
        name: pokemon.name,
        image: `${pokemon.sprites.front_default}`,
        type: pokemonType
    };

};


fetchData()
</script>

   
<style scoped>

</style>