{#if showGreeting}
<h2>Hello {fullName}</h2>
{/if}
<script>
    export let greeting
    $: fullName = `${greeting.firstName} ${greeting.lastName}`
    $: showGreeting = greeting.firstName !== undefined && greeting.lastName !== undefined
</script>