<script>
import Menu from './containers/Menu.vue'
import Clientes from './containers/Clientes.vue'
import Produtos from './containers/Produtos.vue'

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
    },
};

</script>

<template>
    <Menu :selectedTab="selectedTab" @changeTab="changeTab" />
    <div class="container">
        <Clientes v-if="selectedTab === 'clientes'" />
        <Produtos v-else-if="selectedTab === 'produtos'" />
    </div>
</template>
