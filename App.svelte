<script>
  import ServiceList from './components/ServiceList.svelte';

  let services = [
    { id: 1, name: 'General Checkup', description: 'A basic health checkup', price: 50 },
    { id: 2, name: 'Blood Test', description: 'Complete blood count', price: 30 },
  ];

  let newService = { name: '', description: '', price: '' };
  let nextId = services.length + 1;

  function addService() {
    if (!newService.name || !newService.description || !newService.price) {
      alert('All fields are required');
      return;
    }

    services = [
      ...services,
      { ...newService, id: nextId++ }
    ];

    newService = { name: '', description: '', price: '' };
  }

  function deleteService(id) {
    services = services.filter(service => service.id !== id);
  }

  function updateService(updatedService) {
    services = services.map(service =>
      service.id === updatedService.id ? updatedService : service
    );
  }
</script>

<style>
  form { margin-bottom: 20px; }
  input { margin-right: 10px; }
  button { margin-left: 5px; }
</style>

<h1>Healthcare Services</h1>

<form on:submit|preventDefault={addService}>
  <input bind:value={newService.name} placeholder="Service Name" />
  <input bind:value={newService.description} placeholder="Description" />
  <input type="number" bind:value={newService.price} placeholder="Price" />
  <button type="submit">Add Service</button>
</form>

<ServiceList {services} onDelete={deleteService} onUpdate={updateService} />
