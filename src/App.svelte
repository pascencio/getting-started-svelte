<script>
  import GreetingList from "./components/GreetingList.svelte";
  import GreetingsStore from "./stores/greeting.store";
  import GreetingInput from "./components/GreetingInput.svelte";
  let modal = {
    isActive: false,
    message: undefined,
    title: undefined,
  };
  const add = (event) => {
    GreetingsStore.update((greetings) => {
      greeting = event.detail;
      greeting.id = Date.now().valueOf();
      greetings = [...greetings, greeting];
      greeting = {};
      return greetings;
    });
  };
  const remove = (event) => {
    GreetingsStore.update((greetings) => {
      const data = event.detail;
      console.info("Remove greeting event:", data);
      const item = greetings[data.index];
      greetings.splice(data.index, 1);
      greetings = [...greetings];
      modal.title = "Greeting removed";
      modal.message = `Greeting N° ${data.index + 1} removed: ${
        item.firstName
      } ${item.lastName}`;
      modal.isActive = true;
      return greetings;
    });
  };
  function hideModal() {
    modal.isActive = false;
  }

  $: showModal = "modal" + (modal.isActive ? " is-active" : " ");
</script>

<main class="container content">
  <h1>Greeting Application</h1>
  <div class="columns">
    <div class="column">
      <GreetingInput on:add={add} />
    </div>
  </div>
  <div class="columns">
    <div class="column">
      <GreetingList on:remove={remove} greetings={$GreetingsStore} />
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
