<template>
 <h1>notes</h1>
 <h3>current note</h3>
 <!-- <h4 v-text="userip"></h4> -->
 <h4>{{userip}}</h4>
 <!-- mush template is a bit faster -->
 <form @submit.prevent="newnote" class="nform">
     <input v-model='userip' name="okay" class="nokay" placeholder="add a note">
     <!-- <h2>{{userip}}</h2> -->
     <div class="oof">
     <button>new note</button>
     <button @click="lol">delete</button>
     <button @click="done">delete ALL</button>
     </div>
 </form>
 <ul>
 <div v-for="item in notes" :key="item.id">
     <h3>{{item.content}}</h3>
 </div>
 </ul>
</template>

<script>

import { ref } from 'vue';

export default {
    setup(){
        // object wrapper
        const userip = ref('');
        let notes = ref([]);
        notes.value = JSON.parse(localStorage.getItem("data")) ?? [];
        function newnote(){
            // console.log(userip.value)
            notes.value.push({
                id: 0,
                content: userip.value
            })
            userip.value = '';
            localStorage.setItem("data", JSON.stringify(notes.value));
        }

        function done(){
                notes.value.splice(0,notes.value.length);
                localStorage.clear();
        }
        
        function lol(){
            notes.value.shift();
        }

        return {
            userip,
            notes,
            newnote,
            done,
            lol,
        }
    }
}

</script>

<style>
.nform{
    margin: 5px;
    padding: 5px;
}
.oof{
    padding: 5px;
    color: #2c3e50;
}
button{
    margin: 4px;
    color: #2c3e50;
    box-shadow: -3px 3px green, -2px 2px green, -1px 1px green;
    border: 0.5px solid green;
    cursor: pointer;
    outline: none;
    text-align: center;
    font-family: Avenir, Helvetica, Arial, sans-serif;
    font-weight: bold;

}
button:active{
  transform: scale(0.98); 
  box-shadow: 3px 2px 22px 1px rgba(0, 0, 0, 0.24);
}
.nokay{
    margin: 5px;
    height: 25px;
    outline: none;
}
html{
    background-color: #34495E;
}

::placeholder {
    color: #34495E;
    text-align: center;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background-color: #41B883;
  padding: 40px;
}
</style>
