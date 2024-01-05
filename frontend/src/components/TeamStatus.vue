<template>
    <div class="teamStatus" :class="{'bot-substitution-intent': botSubstitutionIntent, 'disp_left': disp_side === 'left', 'disp_right': disp_side === 'right'}">
        
        <div class="teamNameAndCards" :class="{'team_name_right': disp_side === 'left', 'team_name_left': disp_side === 'right'}">

            <div class="team-name" :class="{'team-yellow': color === 'yellow', 'team-blue': color === 'blue'}">
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
        
        <img :src="logoUrl" alt="team logo" class="team-logo"/>
        
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
        /* border-style: solid;
        border-color: black; */
    }

    .card {
    }

    .teamStatus {
        transition: background-color 500ms ease;
        display: flex;
        /* flex-direction: row; */
        align-items: center;
        margin-inline: 0.1em;
        /* border-style: solid;
        border-color: black; */
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
    }

    .team_name_left {
        align-items: flex-start;
    }

    .team_name_right {
        align-items: flex-end;
    }

    .bot-substitution-intent {
        background-color: #c2c3d0;
    }

    .team-name {
        font-size: 0.5em;
        display: flex;
        flex-direction: column;
        /* border-style: solid;
        border-color: black; */
    }


    .team-logo {
        height: 1.5em;
        margin-inline: 0.2em;
        /* border-style: solid;
        border-color: black; */
    }

    .cardTimers {
        display: block;
        /* border-style: solid;
        border-color: black; */
    }

</style>
