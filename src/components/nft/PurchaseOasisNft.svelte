<script lang="ts">
  import { createEventDispatcher } from 'svelte'
  export let show = false
  const dispatch = createEventDispatcher()
  function close() { dispatch('hide') }
</script>
{#if show}
<div class="cs-shell">
  <div class="cs-icon">ℹ️</div>
  <h2 class="cs-title">Purchase OASIS NFT</h2>
  <p class="cs-body">UI Coming Soon — use the OASIS API from the Developer menu for this functionality.</p>
  <button class="cs-btn" on:click={close}>OK</button>
</div>
{/if}
<style>
.cs-shell{display:flex;flex-direction:column;align-items:center;gap:16px;padding:40px 20px;text-align:center}.cs-icon{font-size:48px}.cs-title{font-family:Orbitron,sans-serif;font-size:18px;color:#fff;margin:0}.cs-body{font-size:13px;color:#7a9bbf;line-height:1.6;margin:0;max-width:340px}.cs-btn{margin-top:8px;background:linear-gradient(135deg,#00c8ff,#0080ff);border:none;border-radius:8px;color:#fff;font-family:Orbitron,sans-serif;font-size:12px;font-weight:700;letter-spacing:.08em;padding:10px 28px;cursor:pointer}
</style>
