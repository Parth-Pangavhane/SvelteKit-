<script>
  import { onMount } from 'svelte';
  import { createEventDispatcher } from 'svelte';
  import StickyNote from '$lib/StickyNote.svelte';

  const dispatch = createEventDispatcher();
  let notes = [{ id: 1 }]; // Initial sticky note

  function createStickyNote() {
    notes = [...notes, { id: notes.length + 1 }];
  }

  onMount(() => {
    dispatch('createStickyNote', { id: 1 });
  });
</script>

<main>
  <button on:click={createStickyNote} class="create-button">Create Sticky Note</button>
  {#each notes as { id } (id)}
    <StickyNote {id} />
  {/each}
</main>

<style>
  main {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: flex-start;
    height: 100vh;
    padding: 2rem;
    background-color: #f4f4f4;
  }

  .create-button {
        padding: 0.5rem 1rem;
  font-size: 1rem;
  background-color: #f44336; /* Red */
  color: #fff; /* White text */
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.2s ease;
    }
  
    .create-button:hover {
        background-color: #d32f2f; /* Darker green on hover */
    }
</style>
