<template>
    <div class="content">
       内容详情
    </div>
</template>

<script>
    export default {
        name: "Blank",
        data() {
            return {}
        },

        props:{},

        mounted() {
        },

        methods: {

        }
    }
</script>

<style lang="scss" scoped>
    .content {
        background: #2c3e50;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        min-height: 90vh;
        font-weight: 600;
        font-size: 32px;
    }

</style>