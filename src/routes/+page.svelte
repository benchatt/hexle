<script>
    import Hexagon from "../Hexagon.svelte";
</script>

<div class="layout">
    <Hexagon x="550px" y="350px" char="O" />
    <Hexagon x="654px" y="350px" char="N" />
    <Hexagon x="602px" y="264px" char="Z" />
</div>

<style>
    *,
    *::before,
    *::after {
        padding: 0;
        margin: 0;
        box-sizing: border-box;
    }

    html {
        font-size: 62.5%;
        font-family: "lato";
    }

    body {
        background: #eee;
    }

    .layout {
        position: relative;
        width: 1200px;
        height: 800px;
        border: solid gray 10px;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
</style>
