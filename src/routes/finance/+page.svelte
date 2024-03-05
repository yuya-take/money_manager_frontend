<script lang="ts">
    import IconAdd from "~icons/mdi/plus"; // 例としてのアイコン。適切なものに置き換えてください。
    import Modal from "./modal.svelte"; // モーダルコンポーネントをインポート
    let isModalOpen = false;

    function toggleModal() {
        isModalOpen = !isModalOpen;
    }
</script>

<div>
    <h1>Finance</h1>
    <!-- 他のコンテンツ -->
    <body>
        <p>ここにコンテンツを追加</p>
    </body>

    <!-- "+"ボタン -->
    <button class="fixed-button" on:click={toggleModal}>
        <IconAdd />
    </button>

    <Modal isOpen={isModalOpen} close={toggleModal} />
</div>

<style>
    /* "+"ボタンのスタイル調整 */
    .fixed-button {
        position: fixed; /* ボタンを画面に固定 */
        bottom: 70px; /* Footerの高さ50px + 20pxのマージン */
        right: 20px; /* 右からの距離 */
        z-index: 1000; /* 他の要素の上に表示 */
        /* ボタンの見た目を調整 */
        background-color: #007bff; /* ボタンの背景色 */
        color: white; /* アイコンの色 */
        border: none; /* 枠線を消す */
        border-radius: 50%; /* 円形にする */
        width: 50px; /* ボタンの幅 */
        height: 50px; /* ボタンの高さ */
        display: flex; /* アイコンを中央に配置するためにflexを使用 */
        align-items: center; /* 垂直方向の中央揃え */
        justify-content: center; /* 水平方向の中央揃え */
        cursor: pointer; /* ホバー時のカーソルを指に */
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2); /* 影をつける */
    }
</style>
