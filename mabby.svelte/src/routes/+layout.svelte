<script>
	import logo from '$lib/assets/logo.gif';
</script>

<div class="grid_container" id="bg">
    <nav>
        <a href="/">
            <img src={logo} alt="mabby1110 logo">
        </a>
        <a href="/voxel">voxel</a>
        <a href="/about">about</a>
        <a href="https://github.com/mabby1110?tab=repositories">git</a>
    </nav>
    <slot/>
</div>