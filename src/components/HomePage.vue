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
                <td>
                    <router-link :to="'/update/'+item.id">Update</router-link>
                    <button v-on:click="deleteResturant(item.id)">delete</button>
                </td>

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

  methods:{
    async deleteResturant(id)
    {
        let result = await axios.delete("http://localhost:3000/resturant/"+id);
        console.warn(result)
        if(result.status==200){
            this.loadData()
        }
    },
    async loadData(){
        let user = localStorage.getItem('user-info');
        this.name = JSON.parse(user).name;
        if(!user){
            this.$router.push({name:'SignUp'})
        }

        let result =await axios.get("http://localhost:3000/resturant");
        console.warn(result);
        this.resturant = result.data;
        }
  },

  async mounted(){
    this.loadData();
    }
};
</script>

<style>
table{
    height:auto;
    width:75%;
}
</style>