<div class="parent">
    <div class="child">
        <h2>hola, soy </h2><h1>mabby</h1>
    </div>
    <div class="child">
        jnfdsjf
    </div>
    <div class="child">
        jnfdsjf
    </div>
</div>

<style>
    .child {
        background-color:lightslategrey;
    }
    .parent {
        display: grid;
        gap: 1rem;

        grid-template-columns: repeat(auto-fit, minmax(15rem, auto));
        grid-auto-rows: 28rem;
    }
</style>