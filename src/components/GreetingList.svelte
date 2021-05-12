<script>
  import { createEventDispatcher } from "svelte";
  const dispatcher = createEventDispatcher();
  export let greetings;
  function dispatchRemoveEvent(id, index) {
    dispatcher("remove", {
      id,
      index,
    });
  }
</script>

<h1>Greeting List</h1>
<table>
  <tr>
    <th>N°</th>
    <th>First name</th>
    <th>Last name</th>
    <th>Actions</th>
  </tr>
  {#each greetings as greeting, index (greeting.id)}
    <tr>
      <td>{index + 1}</td>
      <td>{greeting.firstName}</td>
      <td>{greeting.lastName}</td>
      <td>
        <button
          on:click={dispatchRemoveEvent(greeting.id, index)}
          class="button is-danger"
        >
          <span>Remove</span>
        </button>
      </td>
    </tr>
  {:else}
    <tr>
      <td colspan="4">No greetings yet...</td>
    </tr>
  {/each}
</table>
