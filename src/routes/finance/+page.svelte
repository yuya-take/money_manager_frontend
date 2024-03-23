<script lang="ts">
    import IconAdd from "~icons/mdi/plus"; // 例としてのアイコン。適切なものに置き換えてください。
    import ModalAccountForm from "$lib/components/ModalAccountForm.svelte";
    import type { ModalSettings, ModalComponent } from '@skeletonlabs/skeleton';
    import { getModalStore, TabGroup, Tab } from '@skeletonlabs/skeleton';

    const modalStore = getModalStore();

    // モックデータ
    let accounts = [
        { id: 1, date: '2024-03-10', category: 'Food', amount: -20, description: 'Lunch' },
        { id: 2, date: '2024-03-11', category: 'Salary', amount: 2000, description: 'Monthly salary' },
        // その他の収支データ...
    ];

    let dummy_data = [
        {
            id: 1,
            date: '2024-03-10T12:00:00Z',
            category: 'Food',
            amount: -200,
            description: 'Lunch'
        }, 
        {
            id: 2,
            date: '2024-03-11T12:00:00Z',
            category: 'Salary',
            amount: 2000,
            description: 'Monthly salary'
        },
        {
            id: 3,
            date: '2024-03-12T12:00:00Z',
            category: 'Food',
            amount: -10000,
            description: 'Dinner'
        },
        {
            id: 4,
            date: '2024-03-12T12:00:00Z',
            category: 'Food',
            amount: 1500,
            description: 'Lunch'
        }
    ]

    function modalAccountForm(): void {
        const c: ModalComponent = { ref: ModalAccountForm };
        const modal: ModalSettings = {
            type: 'component',
            component: c,
            title: 'Add New Transaction',
            body: 'Complete the form below and then press submit.',
            response: (r) => {
                console.log('response:', r);
                // ここでモックデータに追加処理を行う
            }
        };
        modalStore.trigger(modal);
    }

    // tabsetのアクティブタブを切り替える
    let tabSet: number = 0;
</script>

<div>
    <h1 class="text-xl font-bold mb-4">Finance</h1>
    <TabGroup
        justify="justify-center"
        hover="hover:variant-soft-primary"
        flex="flex-1 lg:flex-none"
        rounded=""
        border=""
        class="bg-surface-100-800-token w-full"
    >
        <Tab bind:group={tabSet} name="tab1" value={0}>日別</Tab>
        <Tab bind:group={tabSet} name="tab2" value={1}>週別</Tab>
        <Tab bind:group={tabSet} name="tab3" value={2}>月別</Tab>
        <Tab bind:group={tabSet} name="tab4" value={3}>合計</Tab>

        <svelte:fragment slot="panel">
            {#if tabSet === 0}
                <!-- 収支のリスト表示 -->
                <div class="mb-6">
                    {#each accounts as account (account.id)}
                        <div class="flex justify-between items-center bg-gray-100 p-4 rounded-lg mb-2">
                            <div>
                                <p>{account.date} - {account.category} - {account.description}</p>
                            </div>
                            <div>
                                <span class:text-red-500={account.amount < 0} class:text-green-500={account.amount > 0}>
                                    ${account.amount}
                                </span>
                            </div>
                        </div>
                    {/each}
                </div>
            {:else if tabSet === 1}
                (tab panel 2 contents)
            {:else if tabSet === 2}
                (tab panel 3 contents)
            {/if}
        </svelte:fragment>
    </TabGroup>

    <!-- "+"ボタン: 収支の追加 -->
    <button 
        class="btn-icon variant-filled fixed-button" 
        on:click={modalAccountForm}
    >
        <IconAdd />
    </button>
</div>

<style>
    .fixed-button {
        position: fixed; /* ボタンを画面に固定 */
        bottom: 70px; /* Footerの高さ50px + 20pxのマージン */
        right: 20px; /* 右からの距離 */
        z-index: 1000; /* 他の要素の上に表示 */
    }
</style>
