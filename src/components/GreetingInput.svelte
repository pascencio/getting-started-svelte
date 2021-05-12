<script>
  import { createEventDispatcher } from "svelte";
  import GreetingOutput from "./GreetingOutput.svelte";
  const dispatcher = createEventDispatcher();
  const greeting = {
    firstName: undefined,
    lastName: undefined,
  };
  const add = () => {
    dispatcher("add", greeting);
  };
  $: showButton =
    greeting.firstName !== undefined && greeting.lastName !== undefined;
</script>

<div class="field">
  <div class="control">
    <input bind:value={greeting.lastName} placeholder="Lastname" type="text" />
  </div>
</div>
<div class="field">
  <div class="control">
    <input bind:value={greeting.firstName} placeholder="Name" type="text" />
  </div>
</div>
{#if showButton}
  <button on:click={add}>Add</button>
{/if}
<GreetingOutput {greeting} />
