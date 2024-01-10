<script>
import './styles.scss'

export default {
    props: {
        cliente: Object,
    },
};

</script>

<template>
    <section class="card">
        <div class="informacoe">
            <div class="informacoe_linha">
                <p>Nome:</p>
                <p>{{ cliente.nome }}</p>
            </div>
            <div class="informacoe_linha">
                <p>CPF: </p>
                <p>{{ cliente.cpf }}</p>
            </div>
            <div class="informacoe_linha">
                <p>Telefone: </p>
                <p>{{ cliente.telefone }}</p>
            </div>
            <div class="informacoe_linha">
                <p>Email: </p>
                <p>{{ cliente.email }}</p>
            </div>
        </div>
    <div class="acoes">
        <form>
            <label>Ativo?</label>
            <select>
                <option>Sim</option>
                <option>Não</option>
            </select>
        </form>
        <form>
            <label>Associar produto:</label>
            <select>
                <option></option>
                <option></option>
                <option></option>
                <option></option>
            </select>
            <button type="button">Associar</button>
        </form>
        <ul>
            <li>Produto A</li>
        </ul>
    </div>
    </section>
</template>