<template>
  <HelloWorld student='students' />
  <slot />
  <img src="../assets/logo.png" alt="img" id="vueLogo"/>
  <p>
    The number of item(s) is {{ numberOfItems }}, so
    {{
      numberOfItems < 50
        ? "Make a new stocking!"
        : "No stocking needed for now!"
    }}
  </p>
  <button @click="increment">Increase items</button>
  <button @click="decrement">Decrease items</button>
  <div class="students">
    <div v-for="student of students" :key="student.id">{{ student.name }} {{ student.class }} {{ student.age }}</div>
  </div>
  <h2>What is your name?</h2>
  <input v-focus v-model="username"/>
  <p>{{ username }}</p>
  <button v-show="username">Submit</button>
  <input @keyup.enter='myGood' v-model="good"/>
  <div>{{ good }}</div>
  <p v-show="state">{{ userGrade }}</p>
  <p v-show="!state">Not true</p>
  </template>
<script>
import HelloWorld from './HelloWorld.vue';
export default {
  name: "TestOne",
  components: {HelloWorld},
  data() {
    return {
      numberOfItems: 50,
      students : [
        {id: 1, name: 'Mike Adeshina', class: 'Grade1', age: 10},
        {id: 2, name: 'John Agboola', class: 'Grade3', age: 15}
      ],
    username: '',
    good: '',
    user: {
      name: 'John',
      grades: {
        primary: 'Grade1',
        secondary: 'Grade3',
        tertiary: 'Grade3'
      }
    },
    state: true,
    };

  },
  methods: {
    increment(){
      this.numberOfItems++
    },
    decrement(){
      this.numberOfItems--
    },
    myGood(){
      this.good = 'great!'
    }
  },

  beforeUpdate() {
    console.log("before update called");
  },
  updated() {
    console.log("updated called");
  },
  watch: {
    numberOfItems(newValue, oldValue){
      console.log('old value is ' + oldValue, 'new value is ' + newValue )
    }
  },
  computed: {
   userGrade(){
    return this.user.grades.tertiary
   }
  },
  directives: {
    focus: {
      inserted: function (el) {
        el.focus()
      }
    }
  },

};
</script>

<style>
h1 {
  font-size: 24px;
  color: red;
}
#vueLogo{
  width: 50px;
  height: 50px;
}
.students{
  display: flex;
  flex-direction: column;
}
</style>
