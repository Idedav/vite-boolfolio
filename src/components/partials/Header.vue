<script>
  export default {
    name: 'Header',
    data() {
      return {}
    },
    components:{},
    methods: {},
    mounted() {},
    computed: {}
  }
</script>

<template>
  <header>
    <nav>
      <ul>
        <li>
          <router-link :to="{name: 'home'}">Home</router-link>
        </li>
        <li>
          <router-link :to="{name: 'about'}">About Us</router-link>
        </li>
        <li>
          <router-link :to="{name: 'contacts'}">Contacts</router-link>
        </li>
        <li>
          <router-link :to="{name: 'projects'}">Projects</router-link>
        </li>
      </ul>
    </nav>
  </header>
</template>


<style lang="scss" scoped>
header{
  width: 100%;
  text-align: center;
  ul{
    list-style:none;
    li{
      margin: 0 10px;
      display:inline-block;
      a{
        color:white;
        text-decoration: none;
        text-transform:uppercase;
        &.active{
          font-weight: bold;
          color:red;
        }
        &:hover{
          text-decoration:underline;
        }
      }
    }
    
  }
}
.router-link-exact-active{
  font-weight: bold;
  color:red($color: #000000);
}
</style>