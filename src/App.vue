
<template>
  <div id="game">
    <section id="monster" class="container">
      <h2>Monster Health</h2>
      <div class="healthbar">
        <div
            class="healthbar__value"
            :style="monsterWidth">
        </div>
      </div>
    </section>
    <section id="player" class="container">
      <h2>Your Health</h2>
      <div class="healthbar">
        <div
            class="healthbar__value"
            :style="personWidth"
        >

        </div>
      </div>
    </section>
    <section id="controls" v-if="gameResult === null ">
      <button @click="attackMonster">ATTACK</button>
      <button>SPECIAL ATTACK</button>
      <button @click="healPerson">HEAL</button>
      <button>SURRENDER</button>
    </section>

    <section class="container" v-else-if="gameResult==='monsterWon' ">
      <h1> Game Over </h1>
      <h2> Mosnter Won 🥴</h2>
      <button @click="startAgain"> Start Again</button>
    </section>

    <section class="container" v-else-if="gameResult==='personWon' ">
      <h1> congratulation </h1>
      <h2> You won the game 🎉</h2>
      <button @click="startAgain"> Start Again</button>
    </section>


    <section id="log" class="container">
      <h2>Battle Log</h2>
      <ul></ul>
    </section>
  </div>
</template>

<script>
export default {
  data () {
    return {
      monsterHealth : 100 ,
      personHealth : 100 ,
      gameResult : null ,
    }
  } ,
  methods :{
    attackMonster (){
      const attackValue = Math.floor(Math.random() * (12- 5)  + 5 ) ;
      this.monsterHealth  = this.monsterHealth  - attackValue ;
      this.attackPerson () ;
    } ,
    attackPerson (){
      const attackValue = Math.floor(Math.random() * (10- 3)  + 5 ) ;
      this.personHealth  = this.personHealth - attackValue ;
      console.log(this.monsterHealth)
    } ,
    healPerson (){
      const attackValue = Math.floor(Math.random() * (1 + 3)  + 5 ) ;
      this.personHealth  = this.personHealth + attackValue ;
      console.log(this.personHealth)
    }
  } ,

  computed:{
    monsterWidth (){
      if(this.monsterHealth < 0) {
        return {'width' : '0%'}
      }
      return {'width' : this.monsterHealth + '%'}
    } ,
    personWidth (){
      if (this.personHealth < 0) {
        return  {'width' : '0%'}
      }
      if(this.personHealth > 100){
        return {'width' : 100 + '%'}
      }
      return {'width': this.personHealth + '%'}  ;
    } ,
    startAgain(){
      this.gameResult = null
      this.monsterHealth =100
      this.personHealth = 100
    }
  } ,
  watch : {
    personHealth( value){
      if( value <= 0 && this.monsterHealth <= 0){
        this.gameResult = 'draw'
      }
      if( value <= 0 ){
        this.gameResult = 'monsterWon'
      }
    } ,
    monsterHealth (value) {
      if(value <=0 && this.personHealth <= 0){
        this.gameResult = 'draw'
      }
      if(value <= 0){
        this.gameResult  = 'personWon'
      }
    }
  }
}
</script>



<style>
  @import "../src/css/styles.css";
</style>
