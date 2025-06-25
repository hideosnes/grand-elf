<script lang="ts">
  import { onMount } from 'svelte';

  let message: string;

  onMount(() => {
    message = 'Welcome to my Svelte app!';
  });
</script>

<main>
  <h1>{message}</h1>
  <p>This is the main entry point of the application.</p>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
  }
</style>