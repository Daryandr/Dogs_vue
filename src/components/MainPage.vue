<template>
  <div class="main">
    <h1>My dogs</h1>
    <button class="add" @click="addDog">+</button>
    <ul class="doglist">
      <li v-for="(dog,index) in dogs" :key="index">
        <DogCard :name="dog.name"
                 :breed="dog.breed"
                 :gender="dog.gender"
                 :birthday="dog.birthday"
                 @deleteDog = "deleteDog(index)"
                 @editDog = "editDog(index,$event)"
        />
      </li>
    </ul>
  </div>
</template>

<script>
import DogCard from "./DogCard"

export default {
  name: 'MainPage',
  components: {DogCard},
  data(){
    return{
      dogs:[
        { name: "Gesta",
          breed: "Estonian Hound",
          gender: "Female",
          birthday: new Date('2021-12-17T00:00:00')
        },
        {name: "Lima",
          breed: "Pug",
          gender: "Female",
          birthday: new Date('2020-02-27T00:00:00')
        }
      ]
    }
  },
  methods: {
    deleteDog(index){
      this.dogs.splice(index,1)
    },
    editDog(index,d){
      this.dogs.splice(index, 1, d);
    },
    addDog(){
      this.dogs.push({name: "",
        breed: "",
        gender: "",
        birthday: new Date()
      })
    }
  }
}
</script>

<style scoped lang="less">
@import '../styles/first.less';
</style>
