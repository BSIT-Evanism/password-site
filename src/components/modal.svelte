<script>
  import Password from "./Password.svelte";
  import Time from "./time.svelte";

  export let name2 = "";
</script>

<Time name={name2} />
<div>
  {#if name2 === ""}
    <div class="d-grid gap-2 col-6 mx-auto">
      <button
        type="button"
        class="btn btn-primary m-2"
        data-bs-toggle="modal"
        data-bs-target="#exampleModal"
      >
        Input your name
      </button>
    </div>
  {/if}
  <div
    class="modal fade"
    id="exampleModal"
    tabindex="-1"
    aria-labelledby="exampleModalLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h1 class="modal-title fs-5" id="exampleModalLabel">Modal title</h1>
          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
          />
        </div>
        <div class="modal-body">
          <div class="form-floating flex-nowrap">
            <input
              bind:value={name2}
              type="text"
              class="form-control"
              placeholder="Username"
              aria-label="Username"
              aria-describedby="addon-wrapping"
            />
            <label for="floatingInput">Your First Name</label>
          </div>
        </div>
        <div class="modal-footer">
          <button
            type="button"
            class="btn btn-secondary"
            data-bs-dismiss="modal">Submit</button
          >
        </div>
      </div>
    </div>
  </div>
</div>
<Password finPass={name2} />
