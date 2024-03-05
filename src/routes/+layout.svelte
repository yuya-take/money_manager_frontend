<script lang="ts">
	import '../app.postcss';

	// Highlight JS
	import hljs from 'highlight.js/lib/core';
	import 'highlight.js/styles/github-dark.css';
	import { AppShell, storeHighlightJs } from '@skeletonlabs/skeleton';
	import xml from 'highlight.js/lib/languages/xml'; // for HTML
	import css from 'highlight.js/lib/languages/css';
	import javascript from 'highlight.js/lib/languages/javascript';
	import typescript from 'highlight.js/lib/languages/typescript';

	hljs.registerLanguage('xml', xml); // for HTML
	hljs.registerLanguage('css', css);
	hljs.registerLanguage('javascript', javascript);
	hljs.registerLanguage('typescript', typescript);
	storeHighlightJs.set(hljs);

	// Floating UI for Popups
	import { computePosition, autoUpdate, flip, shift, offset, arrow } from '@floating-ui/dom';
	import { storePopup } from '@skeletonlabs/skeleton';
	storePopup.set({ computePosition, autoUpdate, flip, shift, offset, arrow });

	import Footer from './Footer.svelte';
	import Header from './Header.svelte';
</script>

<div class="app">
	<AppShell>
		<svelte:fragment slot="header">
			<Header />
		</svelte:fragment>
		<main>
			<slot />
		</main>
		<svelte:fragment slot="footer">
			<Footer />
		</svelte:fragment>
	</AppShell>
</div>

<style>
	/* フルハイトコンテナ */
	.app {
		display: flex;
		flex-direction: column;
		height: 100vh; /* ビューポートの高さを100%に設定 */
	}

	/* メインコンテンツ用のスタイル、必要に応じて調整 */
	main {
		flex-grow: 1; /* フレックスアイテムがコンテナの残りのスペースを埋めるようにする */
		overflow-y: auto; /* 必要に応じてスクロールバーを表示 */
		padding-top: var(--header-height); /* ヘッダーの高さ、変数は実際の値に置き換えてください */
		padding-bottom: var(--footer-height); /* フッターの高さ、変数は実際の値に置き換えてください */
	}

	/* ヘッダーとフッターのスタイルはプロジェクトに合わせて調整 */
	header, footer {
		flex-shrink: 0; /* フレックスアイテムが縮小しないようにする */
	}
</style>
