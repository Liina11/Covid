 <template>
<div>
  <div class="tabs is-centered is-large">
    <ul>
      <li v-for="(item,index) in items"
      :key="index"
      :class="{'is-active': index === active}"
      @click="active = index">
        <router-link :to="item.path">{{item.title}}</router-link>
      </li>
    </ul>
  </div>
  <section class="section">
    <router-view></router-view>
  </section>
</div>
</template>

<script>

export default {  
    created(){
        this.active = this.items.findIndex(item => item.path == this.$route.path);
    },
    data(){
      return {
        active: 0,
        items: [
          {title:'Covid Data ', path:'/'},
          {title:'Infinite Scroll ', path:'/scroll'},
          {title:'Rick and Morty ', path:'/rickandmorty'},
          {title:'Api ', path:'/api'},
          {title:'Clicker ', path:'/clicker'},
          {title:'Modal ', path:'/modal'},
          {title:'ToDo ', path:'todo'},
          {title:'Chart ', path:'chart'},
        ]
      }
    }
}
</script>
<style>
</style>