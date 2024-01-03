<template>
    <div class="teamStatus" :class="{'bot-substitution-intent': botSubstitutionIntent, 'disp_left': disp_side === 'left', 'disp_right': disp_side === 'right'}">
        
        <img :src="logoUrl" alt="team logo" class="team-logo"/>
        
        <div class="teamNameAndCards">

            <div :class="{'team-yellow': color === 'yellow', 'team-blue': color === 'blue'}" class="team-name">
                <div class="team-name-text">{{team.name}}</div>
            </div>
            
            <div class="cards">
                <Card class="card" color="red" :num-cards="team.redCards"/>
                <Card class="card" color="yellow" :num-cards="team.yellowCards"/>
                <Card class="card" color="foul" :num-cards="team.foulCounter"/>
                <BotCount class="card" :num-bots="team.maxAllowedBots"/>
            </div>

            <div class="cardTimers">
                    <span v-for="(cardTime, index) in team.yellowCardTimes.slice(0,3)" :key="index">
                    <CardTimer :cardTimer="cardTime" />
                    </span>
            </div>

        </div>
        
    </div>
</template>

<script>
    import {Referee} from "@/sslProto"
    import teamLogoUrl from "@/teamLogoUrl"
    import Card from "./Card";
    import CardTimer from "./CardTimer";
    import BotCount from "@/components/BotCount";

    export default {
        name: "TeamStatus",
        components: {BotCount, Card, CardTimer},
        props: {
            color: String,
            disp_side: String,
            team: Referee.ITeamInfo,
        },
        computed: {
            logoUrl() {
                return teamLogoUrl(this.team.name);
            },
            botSubstitutionIntent() {
                return this.team.botSubstitutionIntent;
            }
        }
    }
</script>

<style scoped>

    .cards {
        display: flex;
        justify-content: center;
    }

    .card {
    }

    .teamStatus {
        transition: background-color 500ms ease;
        display: flex;
        /* flex-direction: row; */
        align-items: center;
        margin: auto;
        border-style: solid;
        border-color: rgb(101, 100, 100);
    }

    .disp_left {
        flex-direction: row-reverse;
    }

    .disp_right {
        flex-direction: row;
    }

    .teamNameAndCards {
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .bot-substitution-intent {
        background-color: #c2c3d0;
    }

    .team-name {
        /* margin-top: 12px;
        margin-bottom: 12px; */
        font-size: 0.5em;
        display: flex;
        flex-direction: column;
        justify-content: flex-end;
    }

    .team-logo {
        max-width: 20%;
    }

    .cardTimers {
        /* margin-top: 6px; */
        display: block;
    }

</style>
