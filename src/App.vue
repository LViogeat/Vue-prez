<script setup>
import OptionParent from './components/OptionParent.vue'
import CompositionParent from './components/CompositionParent.vue'

</script>

<template>
  <main>
    <div class="mode option">
      <h2>Mode option</h2>
      <option-parent></option-parent>
    </div>

    <div class="mode composition">
      <h2>Mode composition</h2>
      <composition-parent></composition-parent>

    </div>


  </main>
</template>

<style>
@import './assets/base.css';

main {
  display: flex;
}

.mode {
  padding: 2rem;
  width: 50%;
}

.option {
  background-color:peachpuff;
}

.composition {
  background-color: aquamarine;
}



</style>
