<script>
import './styles.scss'
import ItemLista from '../../components/ItemListaCliente/index.vue'
import FormCliente from '../../components/FormCadastroCliente/index.vue'

export default {
    emits: ['cadastrar'],

    data() {
        return {
        mostrarFormulario: false,
        clientes: [],
        };
    },
    methods: {
        abrirFormulario() {
            this.mostrarFormulario = true;
        },
        cadastrarCliente(cliente) {
            console.log('Cliente cadastrado:', cliente)
            this.clientes.push(cliente);
            this.mostrarFormulario = false;
        },
    },
    components: {
        FormCliente,
        ItemLista
    },
};
</script>

<template>
    <button @click="abrirFormulario()" class="btn-cadastrar">Cadastrar novo cliente</button>
    <FormCliente v-if="mostrarFormulario" @cadastrar="cadastrarCliente" />
    <ul class="list">
        <li class="list_item">
            <ItemLista v-for="(cliente, index) in clientes" :key="index" :cliente="cliente" />
        </li>
    </ul>
</template>