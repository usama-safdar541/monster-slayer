<template>
    <div id="app">
        <h1 class="heading">{{ title }}</h1>
        <div id="game">
            <section id="monster">
                <h2>Monster health</h2>
                <div class="healthbar">
                    <div :style="monsterBarStyles" class="healthbar__value"></div>
                </div>
            </section>
            <section id="player">
                <h2>Your Health</h2>
                <div class="healthbar">
                    <div :style="playerBarStyles" class="healthbar__value"></div>
                </div>
            </section>
            <section id="controls">
                <button @click="attackMonster"> ATTACK</button>
                <button :disabled="SpecialAttackmod" @click="specialAttack">SPECIAL ATTACK</button>
                <button @click="healPLayer">HEAL</button>
                <button>SURRENDER</button>
            </section>
            <section id="log">
                <h2>Battle Log</h2>
                <ul></ul>
            </section>
        </div>


    </div>
</template>
    
<script>
function getRandom(min, max) {
    return Math.floor(Math.random() * (max - min)) + min;
}

export default {
    data() {
        return {
            title: 'The Monster Slayer Game',
            playerHealth: 100,
            monsterHealth: 100,
            currentRound :0 ,
        }
    },
     computed:{
monsterBarStyles(){
return { width: this.monsterHealth + '%' } ;
},
playerBarStyles(){
    return { width:this.playerHealth + '%' } ;
},
SpecialAttackmod(){
    return this.currentRound % 3 !==0;
}
     },
    methods: {
        attackMonster() {
            this.currentRound++;
            // math.random gives a value bte o and 1
            const attackVAlue = getRandom(5, 10)
            //  const attackVAlue =   MAth.floor(Math.random()* (15-7)) +5;
            this.monsterHealth = this.monsterHealth - attackVAlue;
            // this.monsterHealth  -= attackVAlue   (alternative syntac to above line)
            this.attackPlayer();
        },
        attackPlayer() {
            const attackVAlue = getRandom(8, 19)
            // const attackVAlue =   MAth.floor(Math.random()* (18-9))+8 ;
            this.playerHealth = this.playerHealth - attackVAlue;
        },
        specialAttack(){
              // math.random gives a value bte o and 1
              const attackVAlue = getRandom(15, 30)
            //  const attackVAlue =   MAth.floor(Math.random()* (15-7)) +5;
            this.monsterHealth = this.monsterHealth - attackVAlue;
            // this.monsterHealth  -= attackVAlue   (alternative syntac to above line)
            this.attackPlayer(); 
        this.currentRound++
        },
        healPLayer(){
            const healValue = getRandom(10,20);
            if(this.playerHealth +healValue>100){
                this.playerHealth=100;
            }else{
            this.playerHealth = this.playerHealth + healValue;
        }
    }
    }
}
</script>
<style scoped>
.heading {
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
    padding: 0.5rem;
    background-color: #880017;
    color: white;
    text-align: center;
    margin-bottom: 2rem;
}

section {
    width: 90%;
    max-width: 40rem;
    margin: auto;
}

.healthbar {
    width: 100%;
    height: 40px;
    border: 1px solid #575757;
    margin: 1rem 0;
    background: #fde5e5;
}

.healthbar__value {
    background-color: #00a876;
    width: 100%;
    height: 100%;
}


.container {
    text-align: center;
    padding: 0.5rem;
    margin: 1rem auto;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
    border-radius: 12px;
}

#monster h2,
#player h2 {
    margin: 0.25rem;
}

#controls {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
}

button {
    font: inherit;
    border: 1px solid #88005b;
    background-color: #88005b;
    color: white;
    padding: 1rem 2rem;
    border-radius: 12px;
    margin: 1rem;
    width: 12rem;
    cursor: pointer;
    box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.26);
}

button:focus {
    outline: none;
}

button:hover,
button:active {
    background-color: #af0a78;
    border-color: #af0a78;
    box-shadow: 1px 1px 8px rgba(0, 0, 0, 0.26);
}

button:disabled {
    background-color: #ccc;
    border-color: #ccc;
    box-shadow: none;
    color: #3f3f3f;
    cursor: not-allowed;
}
</style>  