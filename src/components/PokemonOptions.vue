<template>
    <div class="options-container">
        <ul>
            <li @click="$emit('childMethod',pokemonName[0])">{{pokemonName[0]}}</li>
            <li @click="$emit('childMethod',pokemonName[1])">{{pokemonName[1]}}</li>
            <li @click="$emit('childMethod',pokemonName[2])">{{pokemonName[2]}}</li>
            <li @click="$emit('childMethod',pokemonName[3])">{{pokemonName[3]}}</li>
        </ul>
    </div>
</template>
<script>

export default {
    name: "PokemonOptions",
    props:{
        pokemonName:{
            type: Array,
            default:[],
            required: true,
            validator:(value)=>{
                return value >= 0
            }
        },
        data() {
            return {
            }
        }
    }
}
</script>
<style scoped>
    ul{
        list-style-type: none;
    }
    li{
        background-color: white;
        border-radius: 5px;
        border: 1px solid rgba(0, 0, 0, 2);
        cursor: pointer;
        margin-bottom: 10px;
        width: 250px;
    }
    li:hover{
        background-color: rgba(0, 0, 0, 0.05);
    }
    .options-container{
        display: flex;
        text-align: center;
    }
</style>