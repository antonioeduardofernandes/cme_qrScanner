<script>
  import Table from "./components/Table.svelte"
  import Scanner from "./components/Scanner.svelte"
  let content;

  const readID = (event=>content = event.detail.scannedID)

</script>

<h1>QR Code</h1>
<Scanner on:scanned={readID}/>
<Table content={content}/>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Arial, sans-serif;
    user-select: none;
  }
</style>
