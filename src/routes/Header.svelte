<script lang="ts">
    import { AppBar, AppShell } from '@skeletonlabs/skeleton';
    import { page } from '$app/stores';
    import { goto } from '$app/navigation';
    import IconParkTwotoneSetting from '~icons/icon-park-twotone/setting';

    // ページURLに基づいてタイトルを動的に決定する関数
    $: title = getTitle($page.url.pathname);

    function getTitle(pathname: string): string {
        switch (pathname) {
            case '/':
                return 'Home';
            case '/finance':
                return 'Finance';
            case '/analysis':
                return 'Analysis';
            case '/setting':
                return 'Setting';
            default:
                return 'Unknown Page'; // マッチしない場合のデフォルト値
        }
    }
</script>

<header>
    <AppBar class="flex justify-between w-full px-4">
        <svelte:fragment slot="lead">{title}</svelte:fragment>
        <svelte:fragment slot="trail">
            <button 
                type="button"
                on:click={() => goto('/setting')} 
                class="btn-icon">
                <IconParkTwotoneSetting />
            </button>
        </svelte:fragment>
    </AppBar>
</header>
