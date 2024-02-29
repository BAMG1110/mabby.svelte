<script>
	import logo from '$lib/assets/logo.gif';
</script>

<style>
    img {
        width: 4rem;
        height: 4rem;
        border-radius: 50%;
    }

    .main {
        height: 100vh;
        display: grid;
        grid-template-columns: minmax(10rem, 2fr) minmax(auto, 10fr);
        grid-auto-rows: 1fr 10fr 1fr;
    }
    footer {
        grid-column-start: 1;
        grid-column-end: -1;
    }
</style>

<div class="main">
    <div class="logo">
        <a href="/">
            <img src={logo} alt="mabby1110 logo">
        </a>
    </div>
    <nav>
        <div class="navbar">
            <a href="/macetas">Macetas</a>
            <a href="/about">about</a>
        </div>
    </nav>
    <div class="sidebar">
        sidebar
    </div>
    <div class="content">
        contenido
        <slot/>
    </div>
</div>
<footer>
    footer
</footer>
