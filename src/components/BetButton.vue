<template>
    <div class="button-holder">
        <button @click="makeBet"  class="bet-button" v-bind:class="{ 'for': this.is_for, 'against': !this.is_for }" >{{ this.coefficient }}</button>
    </div>


</template>

<script>
    import axios from 'axios';
    import Vue from 'vue'
    import VueCookies from 'vue-cookies'
    Vue.use(VueCookies);

    export default {
        name: "BetButton",
        props: ["event_id", "is_for", "amount"],
         data(){
            return {
                coefficient: '?'
            }
        },
        methods:{
            async getCoef(){
                const data = (await axios.get(`http://localhost:3000/event/coef?event_id=${this.event_id}&is_for=${this.is_for}`)).data.coef;
                window.console.log(data);
                return data
            },
            async makeBet(){
                const user_id = VueCookies.get('_id');
                if(!user_id){
                    window.console.log(`unauthorized! ${user_id}`)
                    return
                }
                (axios.post(`http://localhost:3000/bet`,{

                        amount: Number.parseInt(this.amount) ,
                        event_id: this.event_id,
                        user_id: user_id,
                        is_for: this.is_for

                }).then((res)=>{
                    window.alert(res.data);
                    this.$emit('bet-done')
                }))
            },
            async updateCoeffs(){
                this.coefficient = (await this.getCoef()) + "";
                this.$emit('balance-changed')
            }
        }
        ,
        async created() {
            this.coefficient = (await this.getCoef()) + "";
            window.console.log("The coef is: "+this.coefficient);
        }
    }
</script>

<style scoped>
    .button-holder{
        width: 35%;
        display:inline-block;
    }

    .bet-button{
        font-size: 1.5em;
    }
    .for {background-color: #008CBA;} /* Blue */
    .against {background-color: #f44336;} /* Red */
</style>