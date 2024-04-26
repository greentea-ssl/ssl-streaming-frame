<template>
    <div class="status-board">
        
        <!-- <hr class="upper-lower-separator"> -->

        <div class="upper-container">
            <TeamStatus class="team-status" disp_side="left" color="yellow" :team="refereeMessage.yellow"/>

            <div class="match-status-container">
                <MatchStatus/>
            </div>

            <TeamStatus class="team-status" disp_side="right" color="blue" :team="refereeMessage.blue"/>
        </div>

        <GameEvents class="lower-container"/>

    </div>
</template>

<script>
    import TeamStatus from "./TeamStatus";
    import MatchStatus from "./MatchStatus";
    import GameEvents from "./GameEvents";

    export default {
        name: "StatusBoard",
        components: {GameEvents, MatchStatus, TeamStatus},
        computed: {
            refereeMessage() {
                return this.$store.state.refereeMsg;
            },
        }
    }
</script>

<style scoped>
    .status-board {
        text-align: center;
        font-size: 3.5vw;
        width: 100%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    .upper-container {
        display: flex;
        justify-content: center;
        width: fit-content;
        border-radius: 0.2em;
        background-color: #353535;
    }

    .lower-container {
    }

    .upper-lower-separator {
        margin-top: 0.1em;
        margin-bottom: 0.1em;
        display: block;
        width: 100%;
    }

    .match-status-container {
        /* flex-grow: 0.4;
        flex-basis: 8%; */
    }

    .team-status {
        /* flex-grow: 0.3;
        flex-basis: 30%; */
    }

</style>
