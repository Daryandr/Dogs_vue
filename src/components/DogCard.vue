<template>
<div class="card">
  <img src="../assets/dog_icon.png" style="width: 12vmin">
  <br v-if="onEdit"/>
  <label v-if="onEdit" for="name-input">Name: </label>
  <input type="text" v-if="onEdit" v-model="dog.name" id="name-input" size="12">
  <h2 v-else style="margin: 0">{{name}}</h2>
  <label v-if="onEdit" for="breed-input"><br/>Breed: </label>
  <input type="text" v-if="onEdit" v-model="dog.breed" id="breed-input" size="12">
  <p v-else>Breed: {{breed}}</p>
  <label v-if="onEdit" for="gender-input"><br/>Gender: </label>
  <select v-if="onEdit" v-model="dog.gender" id="gender-input" style="width:120px">
    <option value="Female">Female</option>
    <option value="Male">Male</option>
  </select>
  <p v-else>Gender: {{gender}}</p>
  <label v-if="onEdit" for="brth-input"><br/>Birthday: </label>
  <input type="date" v-if="onEdit" :value="editDate" @input="setDate($event)" id="brth-input">
  <p v-else>Birthday: {{getDate}}</p>
  <br v-if="onEdit"/>
  <button v-if="onEdit" @click="cancel">CANCEL</button>
  <button v-else @click="editDog">EDIT</button>
  <button v-if="onEdit" @click="submit">SUBMIT</button>
  <button v-else @click="deleteDog">DELETE</button>
</div>
</template>

<script>
export default {
  name: "DogCard",
  props:{
    name: String,
    breed: String,
    gender: String,
    birthday: Date
  },
  data(){
    return{
      onEdit: false,
      dog:{
        name: this.name,
        breed: this.breed,
        gender: this.gender,
        birthday: this.birthday
      }
    }
  },
  computed: {
    getDate: function () {
      return this.birthday.toLocaleDateString()
    },
    editDate: function(){
      const offset = this.dog.birthday.getTimezoneOffset()
      let d = new Date(this.dog.birthday.getTime() - (offset*60*1000))
      return d.toISOString().split('T')[0]
    }
  },
  methods:{
    deleteDog(){
      this.$emit('deleteDog')
    },
    editDog(){
      this.onEdit = true;
    },
    cancel(){
      this.onEdit=false;
      this.dog.name = this.name
      this.dog.breed = this.breed
      this.dog.gender = this.gender
      this.dog.birthday = this.birthday
    },
    submit(){
      this.onEdit=false;
      this.$emit('editDog',this.dog);
    },
    setDate(event){
      this.dog.birthday = new Date(event.target.value)
    },
    addDog(){
      if(this.name == "") this.onEdit = true;
    }
  },
  mounted() {
    this.addDog();
  }
}
</script>

<style lang="less" scoped>
@import '../styles/first.less';
</style>