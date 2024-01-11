<script>
import Menu from './containers/Menu.vue'
import Clientes from './containers/Clientes.vue'
import Produtos from './containers/Produtos.vue'
import ClientesEProdutos from './containers/ClientesEProdutos.vue'

export default {
    data() {
    return {
        selectedTab: 'clientes',
    };
    },
    methods: {
    changeTab(tab) {
        this.selectedTab = tab;
    },
    },
    components: {
        Menu,
        Clientes,
        Produtos,
        ClientesEProdutos,
    },
};

</script>

<template>
    <Menu :selectedTab="selectedTab" @changeTab="changeTab" />
    <div class="container">
        <Clientes v-if="selectedTab === 'clientes'" />
        <Produtos v-else-if="selectedTab === 'produtos'" />
        <ClientesEProdutos v-else-if="selectedTab === 'clientesEprodutos'" />
    </div>
</template>
