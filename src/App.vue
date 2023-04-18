<script setup>
import { ref } from "vue";

const showModal =ref(false)
const newNote =ref("");
const errorMessage= ref("")

const notes = ref([]);
function getRandomColor(){
  return "hsl(" + Math.random() * 360 +", 100% , 75%)";
}
const addNote=() =>{
  if(newNote.value.trim.length < 10){
  return errorMessage.value="note need to be more than 10 character"
 }
 notes.value.push({
  id: Math.floor(Math.random()*1000000),
  text: newMote.value,
  date:new Date(),
  backgroundColor: getRandomColor()
 });
 showModal.value= false;
 newNote.value=""
 errorMessage.value=""
}
</script>
<template>
  <main>
    <div v-if="showModal"  class="overlay">
    <div class="modal">
      <textarea v-model.trim ="newNote" name="note" id="note" cols="30" rows="10"></textarea>
    <p v-if="errorMessage">{{ errorMessage }}</p>
      <button @click="addNote">Add Note</button>
    <button class="close" @click="showModal= false" >close</button>
    </div>
    </div>
    <div class="container">
      <header>
        <h1>notes</h1>
        <button @click="showModal =true">+</button>
      </header  >
     
      <div class="cards-container">
        <div 
        v-for="note in notes"
        :key="note.id"
        class="card"
        :style="{backgroundColor:note.backgroundColor}">
        

    
        <p class="main-text">{{note,text}}</p>

        <p class="date">{{ note.date.toLocalDateString(en-US) }}</p></div>
      
    </div> 
    </div>
  </main>
</template>
<style scoped>
main{
  width: 100vw;
  height: 100vh;
}
.container{
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto

}
header{
  display: flex;
  justify-content: space-between;
  align-items: center;
}


h1{
  font-weight: bold;
  margin-bottom: 20px;
  font-size:75px
}
header button{
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: rgb(21,20,20);
  border-radius: 100%;
  color: white;
  font-size: 20px;
}
.card{
  width: 225px;
  height: 225px;
  background-color:rgb(210, 144, 22);
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-bottom: 20px;
  margin-right: 20px;
}
.cards-container{
  display: flex;
  flex-wrap: wrap;
}

.date{
  font-size: 15px;
  font-weight: bold;
}
.overlay{
  position: absolute;
  width: 100%;
  height: 100%;
  background-color:rgba(0, 0, 0, 0.77);
  z-index: 10;
  align-items: center;
  display: flex;
  justify-content: center;
}
.modal {
  width: 500px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}
.modal button{
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: blueviolet;
  border: none;
  color: rgb(253, 252, 250);
  cursor: pointer;
  margin-top: 15px;

}
.modal .close{
  background-color:red;
  margin-top: 7px;

}
.modal p{
  color: red;
}
</style>