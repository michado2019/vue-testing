<template>
  <div class="mainDiv">
    <TestOne>
    <h2>Your name is {{ name }}</h2>
    <p>Your age is {{ age }}</p>
  </TestOne>
  <button @click='change'>Change</button>
  </div>
</template>

<script>
import TestOne from "./components/TestOne.vue";

export default {
  name: "App",
  components: {
    TestOne,
  },
  data(){
    return{
      name: 'Mike',
      age: '32'
    }
  }, 
  methods: {
   change(){
    this.name = 'Femi',
    this.age = 30
   }
  },
  beforeCreate(){
    console.log('before create called')
  },
  created(){
    console.log('created called')
  },
  beforeMount(){
    console.log('before mount called')
  },
  mounted(){
    console.log('mounted called')
  }
};
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.mainDiv{
 display: flex;
 flex-direction: column;
 align-items: center;
 justify-content: center;
 background-color: #f3f3f3;
}
button{
  background-color: rgb(3, 17, 51);
  border-radius: 5px;
  color: white;
  cursor: pointer;
  width: 100px;
  height: 30px;
}
</style>