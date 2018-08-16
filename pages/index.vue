<template>
  <section class="container">
    <h1 class="title">Music Player</h1>
    <player></player>
  </section>
</template>

<script>
import Player from '../components/Player';

export default {
  components: {
    Player
  }
};
</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding: 24px;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 36px;
  color: #35495e;
  letter-spacing: 1px;
  margin-bottom: 36px;
}
</style>
