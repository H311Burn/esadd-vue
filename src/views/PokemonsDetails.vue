<template>
<div class="grad-color" v-bind:style="getColor">
    <h1>

        Bonjour je suis {{ pokemon.name }} !
        
<div></div>

        </h1>
       <img v-bind:src="pokemon.sprite" alt="" width=10%>
        <div class="containerCenter">
        <p>Types :</p>
       <div v-for="(a,index) in pokemon.types" v-bind:key="index">
         <p class="liste">{{a.type.name}}</p> 
        </div>
       </div>

       <p> PV : {{ pokemon.hp }}</p>
       <p> Attack : {{ pokemon.attack }}</p> 
       <p> Defense : {{ pokemon.defense }}</p>
        <p> Attack Special : {{ pokemon.special_attack }}</p>
        <p> Defense Special : {{ pokemon.special_defense }}</p>
        <p> Vitesse : {{ pokemon.speed}}</p>


        <div class="containerCenter">
            <p>Abilities :</p>
        <div v-for="(a,index) in pokemon.abilities" v-bind:key="index">
         <p class="liste">{{a.ability.name}}</p> 
        </div>
       </div>
       
       </div>
</template>

<script>
import { PokemonService } from '../services/pokemonService'
export default{
    name: 'PokemonDetails',
    data(){
        return{
            pokemonId:0,
            pokemonName:"",
            service: new PokemonService(),
            pokemon:{},
        }
        
    },

    computed:{

        //on recup la couleur en fonctuon du type
    getColor(){
            if (this.pokemon.types != undefined){

                let colors = []

                this.pokemon.types.forEach(t => {

                    //tableau
                    switch (t.type.name) {
                        case 'normal':
                            colors.push('#A7A8A8')
                            break;
                            
                        case 'grass':
                            colors.push('#22B230')
                            break;

                        case 'fire':
                            colors.push('#C6371B')
                            break;
                        
                        case 'water':
                            colors.push('#2762C9')
                            break;
                            
                        case 'fighting':
                            colors.push('#632B06')
                            break;
                            
                        case 'flying':
                            colors.push('#4B729F')
                            break;
                            
                        case 'poison':
                            colors.push('#96169F')
                            break;
                            
                        case 'ground':
                            colors.push('yellow')
                            break;
                            
                        case 'rock':
                            colors.push('brown')
                            break;
                            
                        case 'bug':
                            colors.push('lime')
                            break;
                            
                        case 'ghost':
                            colors.push('darkblue')
                            break;
                            
                        case 'electric':
                            colors.push('yellow')
                            break;
                            
                        case 'psychic':
                            colors.push('pink')
                            break;
                            
                        case 'ice':
                            colors.push('lightblue')
                            break;
                            
                        case 'dragon':
                            colors.push('purple')
                            break;
                            
                        case 'dark':
                            colors.push('black')
                            break;
                            
                        case 'steel':
                            colors.push('grey')
                            break;
                    
                        case 'fairy':
                            colors.push('pink')
                            break;
                            

                        default:
                            break;
                    }
                })
                let result = colors.join(',')

                if(colors.length > 1){
                return 'background : linear-gradient(90deg, '+ result +')';
                }
                else{
                return 'background-color : ' + result
                }
            }
            return ''
            }
        },




    mounted(){
       let route = this.$route
      
       this.pokemonId = route.params.id
       this.service.getPokemon(this.pokemonId).then(pokemon =>{
          
           this.pokemon = pokemon
       })
     
    
       
    }
}
</script>

<style scoped>
.containerCenter {
   display: flex;
   flex-wrap: nowrap;
   text-align: center;
   justify-content: center;
   }

.liste{
    padding-left: 10px;
}
</style>