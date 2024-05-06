<script>
    import { onMount } from "svelte";

    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();

    import { Html5Qrcode } from "html5-qrcode";
    import { store } from "../store";


  onMount(() => {
    const html5QrCode = new Html5Qrcode("reader");
    const config = { fps: 10, qrbox: { width: 250, height: 250 } };
    
    const scannedSuccess = (decodedText, decodedResult) => {
      let scannedID = store.find((e) => e.id == decodedText);
      dispatch('scanned', {
			scannedID
		});
    };
    
    html5QrCode.start({ facingMode: "environment" }, config, scannedSuccess);

  });
</script>

<div id="reader"></div>