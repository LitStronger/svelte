<script>
  import Button,{Label} from '@smui/button';
  import {Separator} from '@smui/list';
  import Checkbox from '@smui/checkbox'
  // import List, { Item, Separator, Text } from '@smui/list';
  let data = [
    {
      id: 0,
      msg: 'eat',
      isChecked: false,
    },
    {
      id: 1,
      msg: 'sleep',
      isChecked: false,
    },
  ]
  let id = 2;
  let msg = '';
  let isChecked = false;
  let isEditing;
  function handleAddClick(){
    id = id + 1;
    if(!msg) msg = '未添加描述';
    let newItem = {id, msg, isChecked};
    data = [...data, newItem]
    msg = ''
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
  <h1>ToDoList with Svelte</h1>
  <!-- <List class="list-wrapper">
    <Item on:SMUI:action={() => {console.log(1)}}><Text>Cut</Text></Item>
  </List> -->
  <ul>
    {#each data as item,index}
      <li>
        <div class="detail">
          <Checkbox bind:checked={item.isChecked}></Checkbox>
          {#if isEditing === index}
            <input type="text" 
              bind:value={data[index].msg} 
              on:blur={() => handleSaveBlur(index)}
            >
          {:else}
            <span class:check={item.isChecked} on:dblclick={() => handleEditClick(index)}>{item.msg}</span>
          {/if}
        </div>
        <div class="action">
          <Button color="secondary" variant="raised" on:click={() => handleEditClick(index)}>
            <Label>Edit</Label>
          </Button>
          <Button color="secondary" variant="raised" on:click={() => handleDelClick(index)}>
            <Label>delete</Label>
          </Button>
        </div>
      </li>
    {/each}
    <Separator />
    <input type="text" bind:value={msg} placeholder=" add item ">
    <Button color="secondary" variant="raised" on:click={handleAddClick}>
      <Label>add</Label>
    </Button>
  </ul>
</main>

<style>
ul{
  list-style-type: none;
  max-width: 600px;
  border: 1px solid var(--mdc-theme-text-hint-on-background, rgba(0, 0, 0, 0.1));
  padding: 1em 1em 0 1em;
}
li{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  width: 100%;
  margin-bottom: 0.5em;
}
input{
  margin-top: 0.5em;
}
.detail{
  display: flex;
  align-items: center;
}
.action{
  background-color: none;
}
.check{
  text-decoration: line-through;
  color: rgb(184, 184, 184);
}
</style>
