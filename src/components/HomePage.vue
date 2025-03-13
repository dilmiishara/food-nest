<template>
    <HeaderCom/>
    <h1>Hello User, Welcome on Home Page </h1>
</template>

<script>
import HeaderCom from './HeaderCom.vue'

export default {
  name: "HomePage", 
  components:{
    HeaderCom
  },

  mounted(){
    let user = localStorage.getItem('user-info');
    if(!user){
        this.$router.push({name:'SignUp'})
    }
}
};
</script>