<script>
import OptionChild from './OptionChild.vue'
export default {
  components: { OptionChild },
  data() {
    return {
      count: 0,
      parentText: '',
      randomNumber: 0,
      stuffs: [
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
      ],
      success: 'rgb(6, 156, 6)',
      danger: 'rgb(216, 4, 4)',
    }
  },
  computed: {
    isStarted() {
      return this.count > 0 ? true : false
    },
  },
  methods: {
    handleClick() {
      this.count++
    },
    getRandomNumber(payload) {
      this.randomNumber = payload
    },
    isMuchLiked(numberOfLike) {
      return numberOfLike > 50 ? true : false
    },
    isMuchDisliked(numberOfDislike) {
      return numberOfDislike > 50 ? true : false
    },

  },
}
</script>

<template>
  <div class="flex-column">
    <div  style="padding-bottom: 1rem;">
      <div class="counter">
        <p>
            Compteur : {{ count }}
        </p>
        <p>
            <button @click="handleClick">Incrémenter</button>
        </p>
      </div>
      <div>
        <option-child
          :isStarted="isStarted"
          :count="count"
          v-model:parentText="parentText"
          @randomNumber="getRandomNumber">
        </option-child>
      </div>
      <div class="textEmit" style="margin-bottom: 2rem;">
        <div style="display: flex;">
          <input type="text" v-model="parentText">
          <p>{{randomNumber}}</p>
        </div>
        <p> Parent text : {{ parentText }}</p>
      </div>
    </div>
    <div class="flex-column animals">

      <div class="flex-column" v-for="stuff in stuffs" v-bind:key="stuff">
        <img class="image" :src="stuff.image">
        <h3>{{ stuff.name }}</h3>
        <div class="flex-row">
          <p v-bind:class="{'success': isMuchLiked(stuff.likes)}">J'aime : {{ stuff.likes }}</p>
          <p v-bind:class="{'danger': isMuchDisliked(stuff.dislikes)}">J'aime pas : {{ stuff.dislikes }}</p>
        </div>
      </div>
    </div>
  </div>


</template>

<style lang="css">
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
    background-color: v-bind(success);
  }

  .danger {
    background-color: v-bind(danger);

  }

 .image {
   width: 200px;
 }
</style>