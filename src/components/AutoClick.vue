<template>
  <button class="button is-warning" @click="autoClick" :disabled="clicks<cost">
      {{name}} ({{cps}} clicks per second) cost: {{cost}} clicks
  </button>
</template>

<script>
export default {
    props: ['cost', 'cps', 'name', 'clicks', 'index'],
    methods: {
        autoClick(){
            this.$emit('clicked', this.index);
        }
    }
}
</script>

<style>
</style>