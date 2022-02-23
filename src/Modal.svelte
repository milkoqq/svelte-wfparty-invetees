<script>
  export let showModal = false;
  export let isSuccessModal = false;
</script>

{#if showModal}
  <div class="modal-outer" on:click|self>
    <div class="modal-inner" class:modal-success={isSuccessModal}>
      <div class="modal-content">
        <slot />
      </div>
    </div>
  </div>
{/if}

<style>
  .modal-outer {
    width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    left: 0;
    z-index: 1;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal-inner {
    background-color: white;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    padding: 1.2rem 3rem;
  }

  .modal-content {
    text-align: left;
  }

  .modal-success {
    background-color: palegreen;
  }
</style>
