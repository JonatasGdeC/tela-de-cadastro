<script>
import  './styles.scss'

export default {
    props: {
        produto: Object,
    },
};
</script>

<template>
    <section class="card">
        <div class="informacoe">
            <div class="informacoe_linha">
                <p>Produto: </p>
                <p>{{ produto.nome }}</p>
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
        </div>
    </section>
</template>