<template>
    <div>
        <b-navbar id="cabecalho">
            <a href="/Tela-Inicial"><h2>Censo de Produção Agrícola do Brasil</h2></a>
            <!--<img src="../assets/logos/logo.png" alt="" width="70" id="posiciona-logo">-->
        </b-navbar>      
    </div>
</template>

<script>
    export default {
        
    }
</script>

<style scoped>

h2{
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
    text-shadow: 3px 1px 1px rgba(0,0,0,0.5);
    color: white;
}

#cabecalho{
    background: #228B22;
    box-shadow: 5px 5px 5px rgba(0,0,0,0.5);
    opacity: 10px;
    padding-left: 32%;
}

a{
    text-decoration: none;
}

#posiciona-logo{
    margin-left: 55%;
}
</style>
