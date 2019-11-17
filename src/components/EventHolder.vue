<template>
    <div class="centered">
        <div class="event" v-bind:key="event._id" v-for="event in this.events">
<!--            <h6>{{bet._id}}</h6>-->
            <Event v-bind:event="event" v-on:balance-changed="balanceChanged"/>
        </div>
    </div>
</template>

<script>
    import Event from "./Event";
    export default {
        name: "EventHolder",
        components: {Event},
        props: ["events"],
        methods:{
            balanceChanged(){
                this.$emit('balance-changed')
            }
        }
    }
</script>

<style scoped>
    .centered{

    }
    .event{
        margin:2em;
    }
</style>