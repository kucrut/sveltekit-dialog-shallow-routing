<script>
  import { onMount } from 'svelte';

  /** @type {HTMLDialogElement} */
  let el;

  function handle_click( e ) {
    // We're only targeting the dialog element itself and its pseudo ::backdrop.
    if ( e.target === el ) {
      e.preventDefault();
      el.close();
    }
  }

  onMount( () => {
    // So we can have the ::backdrop and style it.
    el.showModal();
  } )
</script>

<svelte:body on:click={handle_click} />

<dialog bind:this={el} on:close>
  <div>
    <slot/>
  </div>
</dialog>

<style>
  dialog {
    /* Remove all paddings so the clicking inside the dialog box doesn't close it. */
    padding: 0;
  }

  dialog::backdrop {
    background-color: black;
    opacity: 0.9;
  }

  div {
    padding: 1rem;    
  }
</style>