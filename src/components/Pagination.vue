<template>
    <nav class="pagination is-centered" role="navigation" aria-label="pagination">
    <a class="pagination-previous" @click="$emit('paginate', current-1)" :disabled="current<=1">Previous</a>
    <a class="pagination-next" @click="$emit('paginate', current+1)" :disabled="current>=count">Next page</a>
    <ul class="pagination-list">
        <li v-for="(page,index) in pages" :key="index">
            <a 
            v-if="page!='...'"
            class="pagination-link"
            :class="{'is-current': page==current}"
            @click="$emit('paginate', page)"
            aria-label="Goto page 1">{{page}}</a>
            <span v-else class="pagination-ellipsis">&hellip;</span>
        </li>
    </ul>
    </nav>
</template>

<script>
export default {
    props: ['current', 'count'],
    computed:{
        pages(){
            let pages = [];
            pages[1] = 1;
            pages[2] = 2;
            pages[3] = 3;
            if(this.current>4){
                pages[4] = '...';
            }
            for(let i = this.current-1;i<=this.current+1;i++){
                if(i>=1 && i<=this.count){
                    pages[i] = i;
                }
            }
            if(this.current<this.count-3){
                pages[this.count-3] = '...';
            }
            pages[this.count-2] = this.count-2;
            pages[this.count-1] = this.count-1;
            pages[this.count] = this.count;
            return pages.filter(item => item);
        }
    }
}
</script>

<style>
</style>