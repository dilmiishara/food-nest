<template>
    <HeaderCom/>
    <h1>Hello User, Welcome on Update Restaurant Page </h1>
</template>

<script>
import HeaderCom from './HeaderCom.vue'

export default {
  name: "UpdateRest", 
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