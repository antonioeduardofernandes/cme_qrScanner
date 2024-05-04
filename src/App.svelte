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

  console.log(store);
</script>

<h1>Leitor de QR Code</h1>
<div id="reader"></div>

{#if content}
  <div id="modal">
    <div class="close_button" on:click={closeModal}>X</div>
    <div class="content">
      <div class="header">
        <h3>{content.label}</h3>
        {#if content.marker}
          <h3>Marcador: {content.marker}</h3>
        {/if}
      </div>
      <table>
        <tr>
          <th>Nome</th>
          <th>Quantidade</th>
        </tr>
        {#each content.items as item}
          <tr>
            <td>{item.label}</td>
            <td class="quantity">{item.quantity}</td>
          </tr>
        {/each}
      </table>
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
    overflow: hidden;
  }

  #modal {
    position: absolute;
    z-index: 9000;
    background-color: black;
    height: 100%;
    width: 100%;
    top: 0;
    left: 0;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .content {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    max-height: 90vh;
    max-width: 90vh;
    padding: 1rem;
    background-color: white;
    overflow: scroll;
  }

  table {
    text-align: left;
  }

  .quantity {
    text-align: center;
  }

  .close_button {
    display: flex;
    text-align: center;
    justify-content: center;
    align-items: center;
    width: 30px;
    height: 30px;
    color: white;
    background-color: red;
    border-radius: 50%;
    position: absolute;
    z-index: 9999;
    top: 30px;
    right: 30px;
  }
</style>
