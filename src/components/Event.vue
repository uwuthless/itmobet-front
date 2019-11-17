<template>
    <div class="wrap">
        <h4 class="text-format">{{this.event.event_name}}</h4>
        <div class="button-wrap">
            <BetButton ref="button" v-bind:event_id="event._id" v-bind:is_for="true" v-bind:amount="amount" v-on:bet-done="updateCoeffs" v-on:balance-changed="balanceChanged"/>
            <BetButton ref="button2" v-bind:event_id="event._id" v-bind:is_for="false" v-bind:amount="amount" v-on:bet-done="updateCoeffs" v-on:balance-changed="balanceChanged"/>
        </div>
        <input class="input-effect" type="number" v-model="amount" placeholder="Amount of bet">

    </div>
</template>

<script>
    import BetButton from "./BetButton";
    export default {
        name: "Event",
        components: {BetButton},
        props: ["event"],
        data(){
            return{
                amount:0
            }
        },
        methods:{
            updateCoeffs(){
                this.$refs.button.updateCoeffs()
                this.$refs.button2.updateCoeffs()
            },
            balanceChanged(){
                this.$emit('balance-changed')
            }
        }
    }
</script>

<style scoped>
    .wrap{
        background-color: #a5b6c4;
        border-radius: 15px;
        width:18%;
        padding: 15px;
        margin: auto;
    }

    .button-wrap{
        margin-bottom: 1.5em;
    }

    .text-format{
        font-size: 2em;
    }


/*    input effect*/
    input{
        background-color: #E4E9ED ;
        font-size: 1.5em;
        border: 1px solid;
    border-radius: 3px;
    -webkit-border-radius: 3px;
    -moz-border-radius: 3px;
    -khtml-border-radius: 3px;

    outline: none;
    width: 50%;
    color: #cccccc;
    font-family: Tahoma;
    }


</style>