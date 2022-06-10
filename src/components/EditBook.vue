<template>


<div>
     <div class="mb-3">
        <label for="exampleFormControlInput1" class="form-label">Name</label>
        <input type="email" class="form-control" v-model="name">
    </div>
    <div class="mb-3">
        <label for="exampleFormControlInput1" class="form-label">Price</label>
        <input type="email" class="form-control" v-model="price">
    </div>
    <div class="mb-3">
        <label for="exampleFormControlTextarea1" class="form-label">Description</label>
        <textarea class="form-control"  rows="3" v-model="description"></textarea>
    </div>

    <div class="mb-3">
      <button type="button" @click="updatebook" class="btn btn-primary">update</button>
    </div>

</div>


</template>

<script>

import axios from "axios";

export default {
     name : "AddBook",
     data() {
      return {
        name : '',
        price:'',
        description:'',
      };
    },

    created()
    {
        this.getBookById();
    },

     methods:{

        async getBookById() 
        {

           try {
           const response =   await axios.get(`http://127.0.0.1:8000/api/books/${this.$route.params.id}`);
            this.name = response.data.book.name;
            this.price = response.data.book.price;
            this.description = response.data.book.description;
        } 
        catch (error) 
        {

             console.log(error);

        }

        },

       async updatebook(){
            try {
                 await axios.put(`http://127.0.0.1:8000/api/books/${this.$route.params.id}`,
                 {
                name:this.name,
                price:this.price,
                description:this.description
                 });
                 this.name="";
                 this.price="";
                 this.description="";
                 this.$router.push('/');
                
            } catch (error) {
                console.log(error);
            }
        },

     },

}



</script>