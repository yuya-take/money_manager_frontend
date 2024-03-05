<!-- Modal.svelte -->
<script>
    export let isOpen = false; // モーダルの開閉状態
    export let close = () => {}; // モーダルを閉じる関
</script>
  
{#if isOpen}
<div class="modal-backdrop">
    <div class="modal-content">
        <button on:click={close}>Close</button>
        <!-- モーダルの中身 -->
        <p>ここにモーダルの内容を追加します。</p>
    </div>
</div>
{/if}
  
<style>
    .modal-backdrop {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.5);
      display: flex;
      justify-content: center;
      align-items: center;
    }
  
    .modal-content {
      background-color: white;
      padding: 20px;
      border-radius: 5px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    }
</style>
  