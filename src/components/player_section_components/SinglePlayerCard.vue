<template>
  <div class="card">
        <i id="player-exit-button" class="fa fa-times" @click="deletePlayer()"></i>
        <div class="card-image" @click="handleClick()">
            <img :src="playerImage" style='height: 19vh; width: 16vw; object-fit: cover; object-position:top; border-top-left-radius: 4.5px; border-top-right-radius: 4.5px;'/>
        </div>
        <div class="card-text" @click="handleClick()">
            <span class="date">{{race}} | {{characterClass}} | level {{level}} </span>
            <h2>{{name}}</h2>
            <h4>{{subtitle}}</h4>
        </div>
        <div class="card-stats">
            <div class="stat">
                <div class="value"><input id="npc-stat-value-input" class="player-hp-input" type="number" :value="hitPoints" max="999" style="width:30px"/></div>
                <div class="type">HP</div>
            </div>
            <div class="stat">
                <div class="value">{{armorClass}}</div>
                <div class="type">AC</div>
            </div>
            <div class="stat">
                <div class="value">{{speed}}</div>
                <div class="type">Speed</div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: "SinglePlayerCard",
    props: ["name", "subtitle", "race", "characterClass", "level", "strength", "dexterity", "constitution", "intelligence", 
        "wisdom", "charisma", "initiative", "armorClass", "passivePerception", 
        "hitPoints", "speed", "playerName", "image", "proficiencyBonus", "actions", "equipment", "ally"],
    created: function() {
        this.playerImage = this.image.toString()
    },
    data() {
        return {
            viewAllStats: false,
            allStats: [],
        }
    },
    methods: {
        handleClick: function() {
            this.$emit("create-large-player-card", this.allStats)
        },
        deletePlayer: function() {
            this.$emit("delete-player-from-player-list", this.allStats)
        }
    },
    mounted() {
        this.allStats = [this.name, this.subtitle, this.race, this.characterClass, this.level, this.strength, this.dexterity, this.constitution, this.intelligence, 
        this.wisdom, this.charisma, this.initiative, this.armorClass, this.passivePerception, 
        this.hitPoints, this.speed, this.playerName, this.image, this.proficiencyBonus, this.actions, this.equipment, this.ally]
    }
}
</script>

<style>
    .card {
        display: grid;
        grid-template-columns: 16vw;
        grid-template-rows: 20vh 10vh 6vh;
        grid-template-areas: "image" "text" "stats";
        border-radius: 4.5px;
        background: var(--bg-secondary);
        box-shadow: 5px 5px 15px rgba(0,0,0,0.9);
        text-align: center;
        transition: 0.5s ease;
        cursor: pointer;
        height: 36vh;
        width: 16vw;
        margin:25px;
        margin-top: 1rem;
    }

    input {
        width: 40px;
    }
    
    .stat {
        line-height: 1.5;
    }

    .card-text {
        grid-area: text;
        margin: 0;
    }
    .card-text .date {
        color: rgb(209, 38, 29);
        font-size:13px;
    }
    .card-text h4 {
        color: grey;
        font-size:15px;
        font-weight: 300;
        margin-top: 0;
    }
    .card-text h2 {
        font-size:28px;
        margin: 0rem;
        margin-top: 1vh;        
    }

    .card-image {
        grid-area: image;
        border-top-left-radius: 4.5px;
        border-top-right-radius: 4.5px;
        background-size: cover;
        background-position: top;
    }

    .card-stats {
        grid-area: stats; 
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        grid-template-rows: 1fr;
        border-bottom-left-radius: 4.5px;
        border-bottom-right-radius: 4.5px;
        background: rgb(209, 38, 29);
    }

    .card-stats .stat {
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
        color: white;
        padding:10px;
    }

    .card:hover {
        transform: scale(1.05);
        box-shadow: 5px 5px 15px rgba(0,0,0,0.6);
    }

    #player-exit-button {
        grid-area: image;
        color: rgb(209, 38, 29);
        position: relative;
        height: 2vh;
        width: 2vh;
        top: 1vh;
        right: 2vh;
        cursor: pointer;
    }

    .value {
        margin-top: -.5vh;
    }

    .type {
        margin-top: 0;
        margin-bottom: .5vh ;
    }




</style>