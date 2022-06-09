<template>


<div>

    <router-Link :to="{ name : 'Create' }" routerLinkActive="router-Link-active">Add Book</router-Link>
<table class="table">
  <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Name</th>
      <th scope="col">Price</th>
      <th scope="col">Description</th>
      <th scope="col">Action</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row" v-for="item in items" :key="item.id">1</th>
      <td>{{item.id}}</td>
      <td>{{item.name}}</td>
      <td>{{item.description}}</td>
      <td> 
         <button type="button" class="btn btn-danger" @click="deleteBook(item.id)">Delete</button>
        <router-link :to="{name:'Edit' , params:{id:itel.id}}" type="button" class="btn btn-warning">Edit</button>
      </td>
    </tr>
  </tbody>
</table>
</div>




</template>


<script>
import axios from "axios";

export default {

     name : "BookList",
     data() {
      return {
        items : [],
      };
     },

     created() {
        this.getBooks();

     },

     methods:{

        async   getBooks(){
             try{

                const response = await axios.get('http://127.0.0.1:8000/api/books');
                this.items = response.data;

             } catch (error) {
                console.log(error);
             }
        },

        async deleteBook(id){

             try {
                 
                 await axios.get('http://127.0.0.1:8000/api/books/${id}');
                 this.getBooks();
  
             }catch (error) {

                   console.log(error);

             }

        }

     }

}


</script>