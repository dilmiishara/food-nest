<template>
    <HeaderCom/>
    <h1>Hello {{name}}, Welcome on Home Page </h1>
    <div>
        <table border="1">
            <tr>
                <!-- <th>ID</th> -->
                <th>Name</th>
                <th>Contact</th>
                <th>Address</th>
                <th>Actions</th>

            </tr>
            <tr v-for="item in resturant" :key="item.id">
                <!-- <td>{{item.id}}</td> -->
                <td>{{item.name}}</td>
                <td>{{item.contact}}</td>
                <td>{{item.address}}</td>
                <td><router-link :to="'/update/'+item.id">Update</router-link></td>

            </tr>
        </table>
    </div>
</template>

<script>
import HeaderCom from './HeaderCom.vue'
import axios from 'axios'

export default {
  name: "HomePage", 
  data() {
    return { 
      name: '',
      resturant:[]
    };
  },

  components:{
    HeaderCom
  },

  async mounted(){
    let user = localStorage.getItem('user-info');
    this.name = JSON.parse(user).name;
    if(!user){
        this.$router.push({name:'SignUp'})
    }

    let result =await axios.get("http://localhost:3000/resturant");
    console.warn(result);
    this.resturant = result.data;

}
};
</script>

<style>
table{
    height:auto;
    width:75%;
}
</style>