<script>
  import Greeting from "./Greeting.svelte";
  import GreetingList from "./GreetingList.svelte";
  let greeting = {};
  let greetings = [];
  function add() {
    greeting.id = Date.now().valueOf();
    greetings = [...greetings, greeting];
    greeting = {};
  }
  function remove(data) {
    greetings.splice(data.index, 1);
    greetings = [...greetings];
  }
  $: show_button =
    greeting.firstName !== undefined && greeting.lastName !== undefined;
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
      {#if show_button}
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
</main>
