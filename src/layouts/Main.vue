<template>
  <div class="container">
    <ul>
      <li>
        <v-link href="/">Home</v-link>
        <v-link href="/ch1">ch1</v-link>
        <v-link href="/ch2">ch2</v-link>
        <v-link href="/ch3">ch3</v-link>
        <v-link href="/ch4">ch4</v-link>
        <v-link href="/ch5">Ch5</v-link>
        <v-link href="/ch6">Ch6</v-link>
        <v-link href="/ch7">ch7</v-link>
        <v-link href="/ch8">ch8</v-link>
        <v-link href="/ch9">Ch9</v-link>
        <v-link href="/ch10">Ch10</v-link>
      </li>
    </ul>

    <slot></slot>
  </div>
</template>

<script>
  import VLink from '../components/VLink.vue'

  export default {
    components: {
      VLink
    }
  }
</script>


