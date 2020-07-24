<template>

  <footer id="game_footer" class="bg-maroon text-red">
    {{name}} {{ version }}
  </footer>

</template>

<script>
  export default {
    props: ['name', 'version'],
  }
</script>