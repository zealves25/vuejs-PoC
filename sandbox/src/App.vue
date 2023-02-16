<script>
export default {
  data() {
    return {
      message: "Hello it works!",
      listOfNumbers: [1, 2, 3, 4, 5, 6],
    };
  },
};
</script>

<template>
  <p v-if="message.length % 2 === 0">Even: {{ message }}</p>
  <p v-else>Odd: {{ message }}</p>
  <ul>
    <li v-for="(n, index) in listOfNumbers" :key="`item-${index}`">{{ n }}</li>
  </ul>
</template>
