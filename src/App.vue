<template>
    <div class="h-screen min-h[100vh] bg-[#1A1A1A]">
     <div class="flex flex-col items-center justify-center px-4 place-content-center">
       <div class="mt-20 w-[400px] mb-6 bg-white rounded-md shadow-md my-7 px-4" v-if="generated">
            <div class="flex items-center justify-center mt-5 mb-3">
               <img :src="picture" :alt="picture" class="rounded-full border-3 border-[#08D843]">
            </div>

         <p class="text text-[#08D843] mb-2">{{ title }} {{  first }} {{  last }}</p>
         
           <p class="text-xs font-bold">Email: {{  email }}</p>
           <div class="flex items-center justify-between gap-10 text-center place-items-center">
                 <p class="text-sm font-bold text-gray-500">Gender:  {{  gender }}</p>  
                 <p class="text-xs text-gray-950">
                    Location : {{  state }} - {{  country }}
 
                 </p>
           </div>
       </div>
 
         <button @click="generate" class="bg-[#08D843] text-white rounded-md shadow-md px-4 py-4 hover:bg-green-500  my-7">Generate Random User</button>
   </div>
    </div>
 </template>
 
 <script>
 export default {
   name: 'HelloWorld',
   
   props: {
     msg: String
   },
 
   data(){
     return {
       user: '',
       title: '',
       first: '',
       last:'',
       email: '',
       location: '',
       age: '',
       nationality:'',
       gender: '',
       generated: false,
       picture: '',
       country: '',
 
     }
   },
   methods: {
     async generate(){
       const  res  = await fetch('https://randomuser.me/api');
       const { results } = await res.json();
       if(results){
         this.generated = true;
         console.log(results);
         this.title = results[0].name.title;
         this.first = results[0].name.first;
         this.last = results[0].name.last;
         this.picture = results[0].picture.large;
         this.country = results[0].location.country;
         this.gender = results[0].gender;
         this.email = results[0].email;
         this.state = results[0].location.state;
       }
         //  console.log(results);
     },

    
   }
 }
 </script>
 
 <!-- Add "scoped" attribute to limit CSS to this component only -->
 <style scoped>
 </style>
 