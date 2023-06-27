<script>
  import { onMount } from "svelte";
  export let finPass;
  let pass2;
  let bool = false;
  let bool2 = false;
  let bool3 = false;
  let count = 3;
  let time = new Date();
  let htm;
  let ht;

  $: hours = time.getHours() - 12;
  $: minutes = time.getMinutes();

  $: pass3 = finPass + hours + minutes;
  function checkPass(fin) {
    console.log(fin);
    console.log(hours);
    console.log(pass3);
    console.log(finPass);
    if (fin === pass3) {
      bool = true;
      bool2 = false;
      bool3 = false;
    } else if (fin === "") {
      bool2 = true;
    } else {
      bool3 = true;
      count -= 1;
    }
  }

  $: {
    if (count === 0) {
      location.href = "/blocked";
    } else if (bool === true) {
      location.href = "/welcome";
    }
  }

  onMount(() => {
    const interval = setInterval(() => {
      time = new Date();
    }, 1000);

    return () => {
      clearInterval(interval);
    };
  });

  $: {
    if (count === 3) {
      htm = "div";
    } else if (count === 2) {
      htm = "h2";
    } else if (count === 1) {
      htm = "h1";
      ht = "text-danger";
    }
  }

  $: str = `<${htm} class="${ht}">please put the right password</${htm}>`;
</script>

<div class="container mt-5 p-5">
  {@html str}
  <div class="form-floating">
    <input
      bind:value={pass2}
      type="password"
      class="form-control"
      id="floatingPassword"
      placeholder="Password"
    />
    <label for="floatingPassword">Password</label>
    {#if finPass === ""}
      <h3>Please input your name first</h3>
    {:else}
      <div class="d-grid gap-2 col-6 mx-auto">
        <button
          on:click={checkPass(pass2)}
          type="submit"
          class="btn btn-primary mt-3">Submit</button
        >
      </div>
    {/if}
  </div>
</div>
{#if count === 1}
  <h2>Hint: add your name alongside the time today</h2>
{/if}

{#if bool === true}
  <h1>Welcome</h1>
{:else if bool2 === true}
  <h1>Please input a proper password</h1>
{:else if bool3 === true}
  <h1>Wrong Password!! (remaining tries: {count})</h1>
{/if}
