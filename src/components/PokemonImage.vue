<template>
    <div class="pokemon-container">
        <img :src="negro" class="hidden-pokemon"/>
        <img :src="show" class="fade-in"/>
    </div>
</template>
<script>
export default {
    props:{
        pokemonId:{
            type: Number,
            default:0,
            required: true,
            validator:(value)=>{
                return value >= 0
            }
        },
        showPokemon: {
            type: Boolean,
            default:true,
            required: true,
            validator:(value)=>{
                return value >= 0
            }
        },
    },
    name:'PokemonImage',
    data(){
        return{
            
        }
    },
    computed:{
        negro(){
            return 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/'+this.pokemonId+'.svg'
        },
        show(){
            if(this.showPokemon==true){
                return 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/'+this.pokemonId+'.svg'
            }else{
                return 
            }
        }
    }
}
</script>
<style scoped>
    .pokemon-container{
        height: 200px;
    }
    img{
        height: 200px;
        position: absolute;
        right: 32%;
        user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        -webkit-user-drag: none;
        -webkit-user-select: none;
    }
    .hidden-pokemon{
        filter:brightness(0);
    }
</style>