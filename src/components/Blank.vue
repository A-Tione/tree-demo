<template>
    <div class="content">
        <div>搜索框</div>
        <div>table</div>
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
        height: 600px;
    }

</style>