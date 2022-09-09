<template>
    <h1>¿Quien es este pokemon?</h1><br/>
    <PokemonImage :pokemonId="dato" :showPokemon='resultado'/><br/>
    <PokemonOptions @childMethod="checkData($event)" :pokemonName="names"/><br/>
    <button @click="callNames">Otro pokemon ></button><br/>
    <p>{{respuesta}}</p>
</template>
<script>
    
import PokemonImage from '../components/PokemonImage.vue';
import PokemonOptions from '../components/PokemonOptions.vue';
export default {
    components: { 
        PokemonImage, 
        PokemonOptions 
    },
    name: "PokemonPage",
    data() {
        return {
            resultado: false,
            pokemons: new Array(650),
            numbersPokemons: [],
            lastPokemons:[{id:0,
            name:""}],
            names:[],
            dato:0,
            index:0,
            respuesta:"",
            validador:""
        }
    },
    methods:{
        checkData(data){
            for(var i=0;i<this.lastPokemons.length;i++){
                if(this.dato==this.lastPokemons[i].id){
                    this.index=i
                }
            }
            if(data==this.lastPokemons[this.index].name){
                this.respuesta="Correcto, si era ese pokemon"
            }else{
                this.respuesta="Por poco, en realidad era "+this.lastPokemons[this.index].name
            }
            this.resultado=true
        },
        async callNames(){
            this.resultado=false
            this.respuesta=""
            this.pokemons = Array.from( this.pokemons, (x,idx) => idx+1)
            for(var i=0;i<4;i++){
                let pokemon=Math.floor(Math.random()*this.pokemons.length)
                this.numbersPokemons[i]=pokemon
            }

            const [data1, data2, data3, data4] = await Promise.all([
                fetch('https://pokeapi.co/api/v2/pokemon/'+this.numbersPokemons[0]+'/'),
                fetch('https://pokeapi.co/api/v2/pokemon/'+this.numbersPokemons[1]+'/'),
                fetch('https://pokeapi.co/api/v2/pokemon/'+this.numbersPokemons[2]+'/'),
                fetch('https://pokeapi.co/api/v2/pokemon/'+this.numbersPokemons[3]+'/'),
            ]);

            this.lastPokemons[0] = await data1.json();
            this.lastPokemons[1] = await data2.json();
            this.lastPokemons[2] = await data3.json();
            this.lastPokemons[3] = await data4.json();
            console.log(this.lastPokemons[0])

            this.dato=this.lastPokemons[Math.floor(Math.random()*this.lastPokemons.length)].id
            for (var i=0;i<this.lastPokemons.length;i++){
                this.names[i]= this.lastPokemons[i].name
            }
        }
    },
    mounted(){
        this.callNames()
    }
}
</script>
<style scoped>
    
</style>