<script>
    export let coordinate;
    export let char;
</script>

<div class="tile" {coordinate} on:mouseover on:focus>
    {char}
</div>

<style>
    .tile {
        display: flex;
        justify-content: center;
        align-items: center;
        clip-path: polygon(
            50% 0%,
            100% 25%,
            100% 75%,
            50% 100%,
            0% 75%,
            0% 25%
        );
        background-color: #446666;
        width: 65px;
        height: 75px;
        font-family: Futura, Helvetica, Arial, sans-serif;
        font-size: 46px;
        position: relative;

        color: #1aaeff;
        font-weight: bolder;
    }

    .tile:hover {
        background-color: #cc7908;
        cursor: pointer;
        user-select: none;
    }

    .tile:active {
        background-color: #ffaea1;
        color: #0879cc;
        cursor: pointer;
        user-select: none;
    }
</style>
