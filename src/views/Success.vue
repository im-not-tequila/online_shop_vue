<template>
    <div class="page-succes">
        <div class="columns is-multiline">
            <div class="column is-12">
                <h1 class="title">Спасибо за покупку</h1>

                <p>Ваш заказ будет обработан в течении 48 часов.</p>
            </div>
        </div>
    </div>

</template>

<script>
export default {
    name: 'Success',
    mounted() {
        document.title = 'Заказ оформлен | Мебель'
    },
}
</script>