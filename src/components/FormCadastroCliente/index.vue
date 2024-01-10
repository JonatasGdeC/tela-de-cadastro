<script>
export default {
    data() {
        return {
            nome: '',
            cpf: '',
            telefone: '',
            email: '',
            };
    },
    methods: {
        cadastrar() {
            const dadosCliente = {
                nome: this.nome,
                cpf: this.cpf,
                telefone: this.telefone,
                email: this.email,
            };

            console.log('Emitindo evento cadastrar:', dadosCliente);
            
            this.$emit('cadastrar', dadosCliente);
            this.nome = '';
            this.cpf = '';
            this.telefone = '';
            this.email = '';
            },
        },
    };
</script>

<template>
    <h3>Cadastro de cliente:</h3>
    <form>
        <label for="name">Nome:</label>
        <input v-model="nome" id="name" type="text">
        <label for="cpf">CPF:</label>
        <input v-model="cpf" id="cpf" type="number">
        <label for="contato">Contato:</label>
        <input v-model="telefone" id="contato" type="tel">
        <label for="email">Email:</label>
        <input v-model="email" id="email" type="email">
    </form>
    <button @click="cadastrar">Cadastrar</button>
    <button>Cancelar</button>
</template>