<script>
import './styles.scss'
import ItemListaClienteEProduto from '../components/ItemLista/ClienteEProduto.vue'

export default {
    components: {
        ItemListaClienteEProduto,
    },
    data() {
        return {
        // Inicialize clientesAtivos com a lista armazenada no localStorage ou um array vazio
        clientes: JSON.parse(localStorage.getItem('clientes')) || [],
        produtos: JSON.parse(localStorage.getItem('produtos')) || []
        };
    },
    // Atualize a lista de clientes ativos no localStorage ao montar o componente
    mounted() {
        this.clientes = JSON.parse(localStorage.getItem('clientes')) || [];
        this.produtos = JSON.parse(localStorage.getItem('produtos')) || []
    },
};
</script>

<template>
    <div v-if="clientes.length > 0">
        <ul class="list">
            <li class="list_item">
                <ItemListaClienteEProduto v-for="cliente in clientes" :key="cliente.id" :cliente="cliente" :produtos="produtos"/>
            </li>
        </ul>
    </div>
    <div v-else>
        <h2>Não há clientes ativos</h2>
    </div>
</template>