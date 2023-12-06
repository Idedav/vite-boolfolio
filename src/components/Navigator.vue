<script>

  export default {
    name: 'Navigator',
    props : {
    links : Array
  },
    data() {
      return {
      }
    },
    computed: {},
    mounted() {},
    methods: {
        callApi(linkUrl){
            this.$emit('callApi', linkUrl);
        }
    }
  }
</script>

<template>

<div class="col-12 d-flex justify-content-center">
    <button 
    type="button" 
    v-for="link in links" 
    :key="link.label" 
    v-html="link.label" 
    :disabled="link.active || !link.url"
    @click="callApi(link.url)"
    class="btn btn-secondary mx-1"></button>
</div>


</template>

<style lang="scss" scoped>

</style>