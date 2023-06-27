<script>
  import { onMount } from "svelte";
  let time = new Date();

  export let name;

  $: hours = time.getHours();
  $: minutes = time.getMinutes();
  $: seconds = time.getSeconds();

  onMount(() => {
    const interval = setInterval(() => {
      time = new Date();
    }, 1000);

    return () => {
      clearInterval(interval);
    };
  });
</script>

<h1>hello, {name} this time today is {hours - 12}:{minutes}:{seconds}</h1>
