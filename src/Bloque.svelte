<script>
    let cont=0;

    function handleClick() {
        cont++;
        
    }

</script>

<div class="boton">
    <button on:click={handleClick}>
        Agregar Nota
    </button>
</div>



<div>
    <h6>Usted tiene {cont} notas</h6>
</div>


<style>

</style>