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
    @import "src/assets/styles/_variables";
    .content {
        @include flex-vertical-center;
        flex-direction: column;
        background: #2c3e50;
        min-height: calc(100vh - 60px);
        font-weight: 600;
        font-size: 32px;
    }

</style>