<script>
    import { onMount } from "svelte";
    import {gsap} from 'gsap'
    export let content
    
    const closeModal = () => {
        content = null;
    };
  const tweenIn = node =>{
    gsap.from(node, {opacity:0, duration:.4, scale:.9, ease: "bounce.in"})
  }
</script>

  <!-- <div id="modal">
    <div class="content" >
      <div class="close_button" on:click={closeModal}>X</div>
      <div class="header">
        <h4>Label</h4>
          <h4>Marcador: marker</h4>
      </div>
      <div class="list">
        <div class="list_header">
          <div>Nome</div>
          <div>Quantidade</div>
        </div>
        <div class="items">
         
            <div class="item">
              <div>item</div>
              <div class="quantity">10</div>
            </div>
         
        </div>
      </div>
    </div>
  </div> -->

{#if content}
  <div id="modal">
    <div class="content" in:tweenIn>
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
