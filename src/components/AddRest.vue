<template>
    <HeaderCom/>
    <h1>Hello User, Welcome on Add restaurant Page </h1>
    <form class="add">
      <input type="text" name="name" placeholder="Enter Name" v-model="resturant.name"/>
      <input type="text" name="address" placeholder="Enter Address" v-model="resturant.address"/>
      <input type="text" name="contact" placeholder="Enter Contact" v-model="resturant.contact"/>
      <button type="button" v-on:click="addRest">Add new resturant</button>
    </form>
</template>

<script>
import HeaderCom from './HeaderCom.vue'
import axios from 'axios'

export default {
  name: "AddRest", 
  components:{
    HeaderCom
  },

  data(){
    return{
      resturant:{
        name:'',
        address:'',
        contact:''
      }
    }
  },

  methods:{
    async addRest(){
      console.log(this.resturant)
      const result=await axios.post("http://localhost:3000/resturant",{
        name:this.resturant.name,
        address:this.resturant.address,
        contact:this.resturant.contact
      });

      if(result.status ==201){
        this.$router.push({name:'HomePage'})
      }
      console.warn("result",result)

    }


  },

  mounted(){
    let user = localStorage.getItem('user-info');
    if(!user){
        this.$router.push({name:'SignUp'})
    }
}
};
</script>