<template>
  <ul>
    <li v-for="item in news" :key="item.id">
      {{ item.titel }}
      <span v-if="item.wasRead">!!!</span>
    </li>
  </ul>
</template>

<script>
export default {
  inject: ["titel", "news"],
};
</script>
