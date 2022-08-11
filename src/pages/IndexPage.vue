<template>
  <!--
	Awesome Exercise 1 - Vue.js Basics

	1) Create data properties for name and age
	2) Bind these properties to the two input fields
	3) Display the name and age in the beige box (first line in bold)
	4) Use a computed property to display the age plus 10 years (second line in bold)
	5) Display the number of characters in the name (third line)
	6) Use a filter to display the name in upper case (fourth line)
	7) Only show the beige box if both a name and age have been entered, otherwise, show the red box ("Please enter a name and age.")
	8) Use v-show to only show the error messages next to the fields if the name is longer than 15 characters and the age is greater than 100
	9) Add the class "error" to the input fields if they break the same rules
	10) When the "Generate Random Person" button is clicked, generated a random name (from an array you create) and a random age from 1 - 100. These new values should be reflected everywhere in the view
	11) Create a directive which auto-focuses the name field when the page loads
	12) Make it so a random person is generated when the page first loads

	-->
  <q-page padding>
    <div class="form q-mb-lg">
      <div class="row q-mb-md">
        <label>Name:</label>
        <input type="text" v-model="name" v-bind:class="{'error': name.length > 15}" v-autofocus>
        <label class="error" v-show="name.length > 15">Please enter 15 characters or less</label>
      </div>
      <div class="row q-mb-md">
        <label>Age:</label>
        <input type="number" v-model="age" :class="{'error': age < 1 || age > 100}">
        <label class="error" v-show="age < 1 || age > 100" >Please enter an age between 1 - 100</label>
      </div>
      <div class="row">
        <button @click="randomIdentity">Generate Random Person</button>
      </div>
    </div>
    <div class="description q-mb-lg" v-if="name.length && age.length != 0 ">
      <p>My name is <b>{{name}}</b> and I'm <b>{{age}}</b> years old.</p>
      <p>In 10 years I will be <b>{{plusTenAge}}</b>.</p>
      <p>My name is <b>{{name.length}}</b> characters long.</p>
      <p>My name in uppercase is <b>{{uppercaseName}}</b>.</p>
    </div>
    <div class="no-details" v-else>
      <p>Please enter a name and age.</p>
    </div>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      name: "Joseph",
      age: 54,
      randomName: ["Patrick", "Stephane", "Lorie", "Agathe", "George"]
    }
  },
  computed:{
    plusTenAge(){
      return this.age + 10;
    },
    uppercaseName(){
      return this.name.toUpperCase();
    },
  },
  methods:{
    randomIdentity(){
      this.name = this.randomName[Math.floor(Math.random() * this.randomName.length)]
      this.age = Math.floor(Math.random() * (100 - 1) + 1)
    } 
  },
  directives:{
    autofocus:{
      mounted(el){
        el.focus()
      }
    }
  },
  mounted(){
    this.randomIdentity()
  }
}
</script>

<style>
.form {
  background: #eee;
  padding: 10px;
}

label {
  min-width: 70px;
}

label.error {
  font-size: 13px;
  color: red;
  margin-left: 5px;
  margin-top: 3px;
}

input {
  border: 1px solid #ccc;
}

input.error {
  border: 1px solid red;
  background: pink;
}

.description {
  background: antiquewhite;
  padding: 20px 20px 7px;
}

.no-details {
  background: lightcoral;
  padding: 20px 20px 7px;
}
</style>
