<script>
    import { AppShell, TabGroup, TabAnchor } from '@skeletonlabs/skeleton';
    import { page } from '$app/stores';
    // アイコンコンポーネントをインポート
    import IconParkTwotoneSetting from '~icons/icon-park-twotone/setting';
    import NotoV1MoneyBag from '~icons/noto-v1/money-bag';
    import IconParkAnalysis from '~icons/icon-park/analysis';
    import FlatColorIconsHome from '~icons/flat-color-icons/home';

    // アイコンコンポーネントを含む新しいtabs配列
    const tabs = [
        { href: "/", label: "Home", icon: FlatColorIconsHome },
        { href: "/finance", label: "Finance", icon: NotoV1MoneyBag },
        { href: "/analysis", label: "Analysis", icon: IconParkAnalysis },
        { href: "/setting", label: "Setting", icon: IconParkTwotoneSetting },
    ];
</script>

<footer>
    <TabGroup 
        justify="justify-center"
        active="variant-filled-primary"
        hover="hover:variant-soft-primary"
        flex="flex-1 lg:flex-none"
        rounded=""
        border=""
        class="bg-surface-100-800-token w-full"
    >
        {#each tabs as { href, label, icon }}
            <TabAnchor href={href} selected={$page.url.pathname === href}>
                <div class="tab-anchor-container"> <!-- 修正されたスタイルを適用 -->
                    <svelte:component this={icon} />
                    <span>{label}</span>
                </div>
            </TabAnchor>
        {/each}
    </TabGroup>
</footer>

<style>
    /* タブアンカーのスタイル */
    .tab-anchor-container {
        display: flex;
        flex-direction: column; /* 子要素を縦に並べる */
        align-items: center; /* 中央揃え */
        justify-content: center; /* 中央揃え */
        text-align: center; /* テキストを中央揃え */
        width: 100%;
    }
</style>
