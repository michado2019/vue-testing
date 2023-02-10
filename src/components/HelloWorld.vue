<template>
  <h2>Hello</h2>
  <p>{{ student }}</p>
</template>

<script>
 export default {
   name: "HelloWorld",
   props: ['student']
 }
</script>