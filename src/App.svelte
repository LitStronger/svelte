<script>
  import Button from '@smui/button';
  // import Button from '@smui/button/styled';
  let data = [
    {
      id: 0,
      msg: 'eat',
    },
  ]
  let id = 2;
  let msg = '';
  let isEditing;
  function handleAddClick(){
    id = id + 1;
    let newItem = {id, msg};
    data = [...data, newItem];
    msg = '';
  }
  function handleDelClick(index){
    data.splice(index, 1);
    data = data;
  }
  function handleEditClick(index){
    isEditing = index;

  }
  function handleSaveBlur(index){
    isEditing = false;
  }

</script>

<main>
  <h1>Svelte Component</h1>
  <Button>a</Button>
  <br />
  <ul>
  {#each data as item,index}
    <li>
      {#if isEditing === index}
        <input type="text" 
          bind:value={data[index].msg} 
          on:blur={() => handleSaveBlur(index)}
        >
      {:else}
        <span on:dblclick={() => handleEditClick(index)}>{item.msg}</span>
      {/if}
      <button on:click={() => handleEditClick(index)}>Edit</button> 
      <button on:click={() => handleDelClick(index)}>-</button>
    </li>
  {/each}
  </ul>
  <input type="text" bind:value={msg} placeholder=" add item ">
  <button on:click={handleAddClick}>+</button>
</main>

<style>
ul{
  list-style-type: square;
}

</style>
