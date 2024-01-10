<script>
import Menu from './containers/Menu/index.vue'
import Clientes from './containers/Clientes/index.vue'
import Produtos from './containers/Produtos/index.vue'

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
