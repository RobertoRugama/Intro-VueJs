<template>
  <li><a :href="artist.url" target="_blank">{{ artist.name }}</a> </br>
  <img :src="artist.image[2]['#text']"></li>
</template>

<script>
export default {
  name: 'artist',
  props: [ 'artist' ]

}

</script>

<style scoped>
  li {
  display: inline-block;
  margin: 10px 10px;

}
a{
	margin: 10px;
}
    
</style>
