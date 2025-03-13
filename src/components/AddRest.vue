<template>
    <HeaderCom/>
    <h1>Hello User, Welcome on Add restaurant Page </h1>
</template>

<script>
import HeaderCom from './HeaderCom.vue'

export default {
  name: "AddRest", 
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