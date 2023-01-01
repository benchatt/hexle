<script>
    export let id;
    export let x;
    export let y;
    export let char;
</script>

<div class="tile" style="top: {y}; left: {x};">
    <div class="hexagon">
        <div class="glyph">{char}</div>
    </div>
</div>

<style>
    .tile {
        position: absolute;
    }
    .hexagon {
        width: 57px;
        height: 100px;
        background-color: #3d3d3d;
        position: relative;
        transform: rotate(90deg);
        transition: all 0.2s;
    }

    .hexagon::before {
        content: "";
        display: block;
        border-right: solid #3d3d3d 28px;
        border-top: solid transparent 50px;
        border-bottom: solid transparent 50px;
        position: absolute;
        left: -27.5px;
        top: 0px;
        transition: all 0.2s;
    }

    .hexagon::after {
        content: "";
        display: block;
        border-right: solid #3d3d3d 28px;
        border-top: solid transparent 50px;
        border-bottom: solid transparent 50px;
        position: absolute;
        left: 56px;
        top: -0px;
        transform: scaleX(-1);
        transition: all 0.2s;
    }

    .hexagon:hover::after,
    .hexagon:hover::before {
        border-right: solid #ffae1a 28px;
        transition: all 0.2s;
    }

    .glyph {
        font-family: Futura, Helvetica, Arial, sans-serif;
        font-size: 75px;
        position: relative;
        left: -3.5px;
        top: 6.5px;
        transform: rotate(-90deg);
        color: #1aaeff;
        font-weight: bolder;
    }

    .hexagon:hover {
        background: #ffae1a;
        transition: all 0.2s;
    }
</style>
