<template>
    <div id="find_todo">
        <form @submit.prevent="findEvent">
            <input type="text" v-model="query" name="title" placeholder="Part of event name or tags">
            <input type="submit" value="Submit" class="btn">
        </form>
    </div>

</template>

<script>
    import axios from 'axios';

    export default {
        name: 'FindEvent',
        components: {

        },
        methods: {
            async findEvent(){
                this.$emit('new-events',( await axios.get(`http://localhost:3000/event?query=${this.query}`)).data )

            }
        },
        data(){
            return {
                query:''
            }

        }
    }
</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
