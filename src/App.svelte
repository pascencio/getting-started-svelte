<script>
  import Greeting from "./Greeting.svelte";
  import GreetingList from "./GreetingList.svelte";
  let greeting = {};
  let greetings = [];
  let modal = {
    isActive: false,
    message: undefined,
    title: undefined,
  };
  function add() {
    greeting.id = Date.now().valueOf();
    greetings = [...greetings, greeting];
    greeting = {};
  }
  function remove(event) {
    const data = event.detail;
    console.info("Remove greeting event:", data);
    const item = greetings[data.index];
    greetings.splice(data.index, 1);
    greetings = [...greetings];
    modal.title = "Greeting removed";
    modal.message = `Greeting N° ${data.index + 1} removed: ${item.firstName} ${
      item.lastName
    }`;
    modal.isActive = true;
  }
  function hideModal() {
    modal.isActive = false;
  }
  $: showButton =
    greeting.firstName !== undefined && greeting.lastName !== undefined;
  $: showModal = "modal" + (modal.isActive ? " is-active" : " ");
</script>

<main class="container content">
  <h1>Greeting Application</h1>
  <div class="columns">
    <div class="column">
      <div class="field">
        <div class="control">
          <input
            bind:value={greeting.lastName}
            placeholder="Lastname"
            type="text"
          />
        </div>
      </div>
      <div class="field">
        <div class="control">
          <input
            bind:value={greeting.firstName}
            placeholder="Name"
            type="text"
          />
        </div>
      </div>
      {#if showButton}
        <button on:click={add}>Add</button>
      {/if}
    </div>
  </div>
  <div class="columns">
    <div class="column">
      <Greeting {greeting} />
    </div>
  </div>
  <div class="columns">
    <div class="column">
      <GreetingList on:remove={remove} {greetings} />
    </div>
  </div>
  <div class={showModal}>
    <div class="modal-background" />
    <div class="modal-card">
      <header class="modal-card-head">
        <p class="modal-card-title">{modal.title}</p>
      </header>
      <section class="modal-card-body">
        {modal.message}
      </section>
      <footer class="modal-card-foot">
        <button on:click={hideModal}>Ok</button>
      </footer>
    </div>
  </div>
</main>
