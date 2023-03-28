<script>
     let toDoitem = '';
     let toDoList = [];

     function add(){
          if (toDoitem == '') {
               return;
          }
          toDoList = [...toDoList, {
               text: toDoitem,
               done: false
          }]
          toDoitem= '';
     }
     function removeThis(index) {
          toDoList.splice(index, 1);
          toDoList = toDoList;
     }
     function clearDone(){
          toDoList = toDoList.filter(t => !t.done);
     }

     function clearAll(){
          toDoList =[]
     }
</script>

<form on:submit|preventDefault={add}>
     <input bind:value={toDoitem} type='text' autofocus/><button type="submit">Add</button>
</form>

<ul>
     {#each toDoList as item, index}
          <li>
               <input type='checkbox' bind:checked={item.done}>
               <span class:done={item.done}>{item.text}</span>
               <span on:click={() => removeThis(index)} on:keypress={() => removeThis(index)} class='remove'></span>
          </li>
     {/each}
</ul>
<button on:click={clearDone}>Clear Done</button>
<button on:click={clearAll}>Clear All</button>

<style>
     ul {
          list-style: none;
     }
     .done {
          text-decoration: line-through;
          color: darkgray;
     }
     .remove {
          height: 1rem;
          width: 1rem;
          display: inline-block;
          background: url('./images/trash.png') no-repeat;
          background-size: 100% auto;
          cursor: pointer;
     }
</style>