<template lang="pug">
  li
    h2
        a(:href="artista.url" target="_blank") 
            span {{artista.name}}
    img(:src="artista.image[2]['#text']")
</template>

<script>
export default {
    name: "artista",
    props: ["artista"]
};
</script>

<style lang="scss">
li {
    display: block;
    margin: 10px 0;
}
</style>
