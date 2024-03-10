<script lang="ts">
    import IconAdd from "~icons/mdi/plus"; // 例としてのアイコン。適切なものに置き換えてください。

    import ModalAccountForm from "$lib/components/ModalAccountForm.svelte";

    import type { ModalSettings, ModalComponent } from '@skeletonlabs/skeleton';
    import { getModalStore } from '@skeletonlabs/skeleton';
	const modalStore = getModalStore();

    function modalAccountForm(): void {
		const c: ModalComponent = { ref: ModalAccountForm };
		const modal: ModalSettings = {
			type: 'component',
			component: c,
			title: 'Custom Form Component',
			body: 'Complete the form below and then press submit.',
			response: (r) => console.log('response:', r)
		};
		modalStore.trigger(modal);
	}
</script>

<div>
    <h1>Finance</h1>
    <!-- 他のコンテンツ -->
    <body>
        <p>ここにコンテンツを追加</p>
    </body>

    <!-- "+"ボタン -->
    <button class="btn-icon variant-filled fixed-button" on:click={modalAccountForm}>
        <IconAdd />
    </button>

</div>

<style>
    /* "+"ボタンのスタイル調整 */
    .fixed-button {
        position: fixed; /* ボタンを画面に固定 */
        bottom: 70px; /* Footerの高さ50px + 20pxのマージン */
        right: 20px; /* 右からの距離 */
        z-index: 1000; /* 他の要素の上に表示 */
    }
</style>
