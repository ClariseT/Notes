<script>
import Logo from "./Logo.svelte";
import Search from "./Search.svelte";
import Settings from "./Settings.svelte";
</script>


<div class="Header">
    <Logo appName="Notas"/>
    <Search on:input/>
    <Settings/>
    
</div>


<style>
    .Header{
        background-color: rgba(0, 38, 255, 0.178);
        border-radius: 10px; 
        margin: 18px;
        padding: 12px;
    }

    

</style>