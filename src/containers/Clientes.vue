<script>
import './styles.scss'
import FormCliente from '../components/FormCadastro/Cliente.vue'
import ItemListaClientes from '../components/ItemLista/Cliente.vue'

export default {
    emits: ['cadastrar'],

    data() {
        return {
        mostrarFormulario: false,
        mensagemBTN: 'Cadastrar',
        clientes: [],
        clientesInativos: [],
        };
    },

    mounted() {
        this.carregarDadosDoLocalStorage();
    },

    beforeUnmount() {
        this.salvarDadosNoLocalStorage();
    },

    methods: {
        carregarDadosDoLocalStorage() {
            const storedClientes = localStorage.getItem('clientes');
            const storedClientesInativos = localStorage.getItem('clientesInativos');
            
            if (storedClientes) {
                this.clientes = JSON.parse(storedClientes);
            }

            if (storedClientesInativos) {
                this.clientesInativos = JSON.parse(storedClientesInativos);
            }
        },

        salvarDadosNoLocalStorage() {
            const jsonStringClientes = JSON.stringify(this.clientes);
            const jsonStringClientesInativos = JSON.stringify(this.clientesInativos);

            localStorage.setItem('clientes', jsonStringClientes);
            localStorage.setItem('clientesInativos', jsonStringClientesInativos);
        },

        btnPrincipal(){
            if(this.mostrarFormulario === false){
                this.mostrarFormulario = true
                this.mensagemBTN = 'Cancelar'
            } else {
                this.mostrarFormulario = false
                this.mensagemBTN = 'Cadastrar'
            }
        },
        cadastrarCliente(cliente) {
            cliente.ativo = true;
            this.clientes.push(cliente);
            this.mostrarFormulario = false;
            this.mensagemBTN = 'Cadastrar'
            // Atualiza o localStorage após cadastrar um novo cliente
            const jsonString = JSON.stringify(this.clientes);
            localStorage.setItem('clientes', jsonString);
        },

        alterarEstadoCliente(cliente){
            cliente.ativo = !cliente.ativo;
            // Move o cliente para a lista de clientes inativos, se estiver inativo
            if (!cliente.ativo) {
                const index = this.clientes.indexOf(cliente);
                if (index !== -1) {
                    this.clientes.splice(index, 1);
                    this.clientesInativos.push(cliente);
                }
            } else {
                // Move o cliente de volta para a lista de clientes ativos, se estiver ativo novamente
                const index = this.clientesInativos.indexOf(cliente);
                if (index !== -1) {
                    this.clientesInativos.splice(index, 1);
                    this.clientes.push(cliente);
                }
            }
            // Atualiza o localStorage após alterar o estado do cliente
            const jsonString = JSON.stringify(this.clientes);
            localStorage.setItem('clientes', jsonString);
        },
        
        excluirClienteDoLocalStorage(cliente){
            const confirmacao = window.confirm("Deseja realmente excluir este cliente?");

            if(confirmacao){
                const index = this.clientes.indexOf(cliente);
                if(this.clientes.includes(cliente)){
                    this.clientes.splice(index, 1);
                    const jsonString = JSON.stringify(this.clientes);
                    localStorage.setItem('clientes', jsonString);
                } else {
                    this.clientesInativos.splice(index, 1);
                    const jsonString = JSON.stringify(this.clientesInativos);
                    localStorage.setItem('clientesInativos', jsonString);
            }
            }
        }
    },
    components: {
        FormCliente,
        ItemListaClientes
    },
};
</script>

<template>
    <button @click="btnPrincipal" class="btn-cadastrar" :class="{'btn-cadastrar--cancelar': mensagemBTN === 'Cancelar'}">{{ mensagemBTN }}</button>
    <FormCliente v-if="mostrarFormulario" @cadastrar="cadastrarCliente" />

    <div v-if="clientes.length > 0 || clientesInativos.length > 0">
        <ul class="list" v-if="clientes.length > 0">
            <li class="list_item">
                <ItemListaClientes v-for="(cliente, index) in clientes" :key="index" :cliente="cliente" @excluir-cliente="excluirClienteDoLocalStorage" @alterar-estado="alterarEstadoCliente" />
            </li>
        </ul>

        <div class="list_inativos" v-if="clientesInativos.length > 0">
            <h3 class="list_title">Clientes Inativos</h3>
            <ul class="list--inativos_card">
                <li class="list_item">
                    <ItemListaClientes v-for="(cliente, index) in clientesInativos" :key="index" :cliente="cliente" @excluir-cliente="excluirClienteDoLocalStorage" @alterar-estado="alterarEstadoCliente" />
                </li>
            </ul>
        </div>
    </div>
    <div v-else class="list_inexistente">
        <h2>Não há clientes cadastrados</h2>
    </div>
</template>