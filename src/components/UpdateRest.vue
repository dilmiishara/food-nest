<template>
    <HeaderCom/>
    <h1>Hello User, Welcome on Update Restaurant Page </h1>

    <form class="add">
      <input type="text" name="name" placeholder="Enter Name" v-model="resturant.name"/>
      <input type="text" name="address" placeholder="Enter Address" v-model="resturant.address"/>
      <input type="text" name="contact" placeholder="Enter Contact" v-model="resturant.contact"/>
      <button type="button" v-on:click="updateRest">Update resturant</button>
    </form>

</template>

<script>
import HeaderCom from './HeaderCom.vue'
import axios from 'axios'

export default {
  name: "UpdateRest", 
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
    async updateRest(){
      console.warn(this.resturant)
      const result = await axios.put("http://localhost:3000/resturant/"+this.$route.params.id,{
        name:this.resturant.name,
        address:this.resturant.address,
        contact:this.resturant.contact,
      })
      if(result.status==200){
        this.$router.push({name:'Home'});
      }
    }

  },

  async mounted(){
    let user = localStorage.getItem('user-info');
    if(!user){
        this.$router.push({name:'SignUp'})
    }
    console.warn(this.$route.params.id)

    const result = await axios.get('http://localhost:3000/resturant/'+this.$route.params.id)
    console.warn(result)

    this.resturant= result.data
}
};
</script>