<script>
  import { Html5Qrcode } from "html5-qrcode";
  import { onMount } from "svelte";
  import { store } from "./store";

  let content;

  onMount(() => {
    const html5QrCode = new Html5Qrcode("reader");
    const config = { fps: 10, qrbox: { width: 250, height: 250 } };

    const scannedSuccess = (decodedText, decodedResult) => {
      content = store.find((e) => e.id == decodedText);
      // html5QrCode.stop()
    };

    html5QrCode.start({ facingMode: "environment" }, config, scannedSuccess);
  });

  const closeModal = () => {
    content = null;
  };
</script>

<h1>Leitor de QR Code</h1>
<div id="reader"></div>

{#if content}
  <div id="modal">
    <div class="content" >
      <div class="close_button" on:click={closeModal}>X</div>
      <div class="header">
        <h4>{content.label}</h4>
        {#if content.marker}
          <h4>Marcador: {content.marker}</h4>
        {/if}
      </div>
      <div class="list">
        <div class="list_header">
          <div>Nome</div>
          <div>Quantidade</div>
        </div>
        <div class="items">
          {#each content.items as item}
            <div class="item">
              <div>{item.label}</div>
              <div class="quantity">{item.quantity}</div>
            </div>
          {/each}
        </div>
      </div>
    </div>
  </div>
{/if}

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Arial, sans-serif;
    user-select: none;
  }

  #modal {
    height: 100vh;
    width: 100vw;
    position: absolute;
    z-index: 9000;
    background-color: rgba(0, 0, 0, 0.9);
    top: 0;
    left: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
  }

  .close_button {
    position: absolute;
    z-index: 9999;
    top: 110px;
    right: 6px;
    display: flex;
    text-align: center;
    justify-content: center;
    align-items: center;
    width: 30px;
    height: 30px;
    color: white;
    background-color: rgb(218, 50, 50);
    border-radius: 50%;
  }

  .content {
    height: 600px;
    width: 340px;
    display: flex;
    flex-flow: column;
    background-color: white;
    justify-content: center;
    align-items: center;
    padding: 1rem;
  }

  .content .header {
    text-transform: uppercase;
  }

  .list {
    width: 100%;
    height: 100%;
    overflow: hidden;
    display: flex;
    flex-flow: column;
    text-transform: capitalize;
  }

  .list_header {
    display: flex;
    background-color: black;
    color: white;
    justify-content: space-between;
    padding: 0.2rem;
  }

  .items {
    overflow: scroll;
  }

  .item {
    display: flex;
    justify-content: space-between;
    padding: 0.2rem;
  }

  .item:nth-child(even) {
    background-color: rgba(173, 226, 222, 0.4);
  }
</style>
