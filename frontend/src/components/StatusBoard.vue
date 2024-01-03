<template>
    <div class="status-board">
        <div class="upper-container">
            <TeamStatus class="team-status" disp_side="left" color="yellow" :team="refereeMessage.yellow"/>

            <div class="match-status-container">
                <MatchStatus/>
            </div>

            <TeamStatus class="team-status" disp_side="right" color="blue" :team="refereeMessage.blue"/>
        </div>

        <hr class="upper-lower-separator">

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
    }

    .upper-container {
        display: flex;
        justify-content: center;
        /* align-items: stretch; */
    }

    .lower-container {
    }

    .upper-lower-separator {
        margin-top: 0.2em;
        margin-bottom: 0.2em;
        display: block;
    }

    .match-status-container {
        flex-grow: 0.4;
        flex-basis: 10%;
    }

    .team-status {
        flex-grow: 0.3;
        flex-basis: 30%;
    }

</style>
