<script>
	import logo from '$lib/assets/logo.gif';
</script>

<style>
    img {
        width: 4rem;
        height: 4rem;
        border-radius: 50%;
    }

    .grid_container {
        height: 100vh;
        display: grid;
        gap: 0.4rem;
        grid-template-columns: repeat(12, 1fr);
        grid-template-rows: repeat(12, 1fr);
        background-image:url('$lib/assets/cross-bg.svg');
		background-size: cover;
    }

    nav {
        background-color:aliceblue;
        grid-area: 1 / 4 / 2 / 10;

        display: flex;
        justify-content: space-evenly;
        align-items: center;
    }

    .title {
        box-sizing: border-box;
        border-style: dashed;
        border-color: black;
        border-width: 1px;
        grid-area: 3 / 3 / 7 / 6;
        z-index: 1;
        min-height: 15rem;

    }

    .preview {
        box-sizing: border-box;
        border-style: dashed;
        border-color: black;
        border-width: 1px;
        grid-area: 3 / 6 / 9 / 11;
        z-index: 1;
        min-height: 28rem;
    }

</style>

<div class="grid_container">
    <nav>
        <a href="https://github.com/mabby1110?tab=repositories">git</a>
        <a href="/">
            <img src={logo} alt="mabby1110 logo">
        </a>
        <a href="/about">about</a>
    </nav>
    <div class="title">
        <h1>Titulo</h1>
    </div>
    <div class="preview">
        <slot/>
    </div>
</div>
