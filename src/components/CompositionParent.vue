<script setup>
    import {ref, computed} from 'vue'
    import CompositionChild from './CompositionChild.vue'
    
    // Début Compteur
    const count = ref(0)
    const isStarted = computed(() =>  {
        return count.value > 0 ? true : false
    })
    
    function handleClick() {
        count.value++
    }
    //Fin Compteur

    //Début message transmis parent-enfant
    const parentText = ref('')
    const randomNumber = ref(0)

    function getRandomNumber(payload) {
      randomNumber.value = payload
    }
    //Fin message transmis parent-enfant

    //Début images
    const stuffs = [
        {
          image: 'https://cdn.pixabay.com/photo/2016/12/05/11/39/fox-1883658_960_720.jpg',
          name: 'Renard',
          likes: 45,
          dislikes: 10
        },
        {
          image: 'https://cdn.pixabay.com/photo/2022/01/11/12/07/animal-6930449_960_720.jpg',
          name: 'Singe',
          likes: 109,
          dislikes: 15
        },
        {
          image: 'https://cdn.pixabay.com/photo/2012/06/19/10/32/owl-50267_960_720.jpg',
          name: 'Hibou',
          likes: 21,
          dislikes: 60
        }        
    ];
    
    function isMuchLiked(numberOfLike) {
      return numberOfLike > 50 ? true : false
    };

    function isMuchDisliked(numberOfDislike) {
      return numberOfDislike > 50 ? true : false
    }
    //Fin images
  
</script>

<template>
    <div class="flex-column">
      <div style="padding-bottom: 1rem;">
        <div class="counter">
          <p>
            Compteur : {{ count }}
          </p>
          <p>
            <button @click="handleClick">Incrémenter</button>
          </p>
        </div>
        <div>
          <composition-child
              :isStarted="isStarted"
              :count="count"
              v-model:parentText="parentText"
              @random-number="getRandomNumber">
            </composition-child>
        </div>
        <div class="textEmit" style="margin-bottom: 2rem;">
          <div style="display: flex;">
            <input type="text" v-model="parentText">
            <p>{{randomNumber}}</p>
          </div>
          <p> Parent text : {{ parentText }}</p>
        </div>
      </div>
    </div>
    <div class="flex-column animals">

      <div class="flex-column" v-for="stuff in stuffs" :key="stuff">
        <img class="image" :src="stuff.image">
        <h3>{{ stuff.name }}</h3>
        <div class="flex-row">
          <p v-bind:class="{'success': isMuchLiked(stuff.likes)}">J'aime : {{ stuff.likes }}</p>
          <p v-bind:class="{'danger': isMuchDisliked(stuff.dislikes)}">J'aime pas : {{ stuff.dislikes }}</p>
        </div>
      </div>
    </div>
</template>

<style scoped>


  ::v-global(.counter) {
    border: 1px solid blue;
  }
  ::v-global(.animals) {
    border: 1px solid red;
  }

  .container {
    display: flex;
    justify-content: space-between;
  }

  .flex-column {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  .flex-row {
    display: flex;
    flex-direction: row;
  }

  p {
    padding: 3px;
  }

  .success {
    background-color: rgb(6, 214, 6);
  }

  .danger {
    background-color: rgb(248, 66, 66);
  }

 .image {
   width: 200px;
 }


</style>