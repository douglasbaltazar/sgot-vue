<template>
    <div id="pedido-new">
        <div class="container mt-2">
            <div class="row">
                <div class="col-12">
                    <h3>Novo Pedido</h3>
                    <hr>
                    <PedidoForm @submit="onSubmit"/>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import PedidoForm from './forms/PedidoForm'
export default {
    name: "PedidoNew",
    components: {
        PedidoForm
    },
    data: () => ({
    }),
    methods: {
        onSubmit(data) {
            console.log(data)
        }
    }
}
</script>

<style>

</style>