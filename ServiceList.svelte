<script>
  export let services = [];
  export let onDelete;
  export let onUpdate;

  let editedService = null;

  function editService(service) {
    editedService = { ...service };
  }

  function saveService() {
    onUpdate(editedService);
    editedService = null;
  }
</script>

<style>
  /* Add some basic styling */
  .service { margin-bottom: 10px; }
  button { margin-left: 10px; }
</style>

{#each services as service}
  <div class="service">
    {#if editedService && editedService.id === service.id}
      <input bind:value={editedService.name} />
      <input bind:value={editedService.description} />
      <input type="number" bind:value={editedService.price} />
      <button on:click={saveService}>Save</button>
    {:else}
      <strong>{service.name}</strong> - {service.description} (${service.price})
      <button on:click={() => onDelete(service.id)}>Delete</button>
      <button on:click={() => editService(service)}>Edit</button>
    {/if}
  </div>
{/each}
