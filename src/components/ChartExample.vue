<template>
<div>
    <button class="button is-primary" @click="addVote">add vote</button>
    <chart :data="votes" type="line" :labels="labels"></chart>
</div>
</template>

<script>
import Chart from './Chart.vue';
export default {
    components: {Chart},
    data(){
        return{
            votes:[12, 19, 1, 5, 69, 3],
            labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],
            types:['bar', 'line', 'radar', 'pie', 'doughnut', 'polarArea', 'bubble', 'scatter'],
            active: 0
        }
    },
    methods: {
        addVote(){
            // this.votes[0]++;
            // this.$set(this.votes, 0, this.votes[0]+1);
            let changedVotes = [...this.votes];
            changedVotes[0]++;
            this.votes = changedVotes;
            // this.votessplice(0,1,this.votes[0]+1)
        }
    }
}
</script>

<style>
</style>