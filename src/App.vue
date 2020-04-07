<template>
    <div id="app">
        <div v-if="isCut" class="app-left">
            <col-table @colCut="cut"></col-table>
        </div>
        <div class="app-right">
            <row-table v-if="!isCut" @rowCut="cut"></row-table>
            <blank></blank>
        </div>
    </div>
</template>

<script>
    import ColTable from "./components/ColTable";
    import RowTable from "./components/RowTable";
    import Blank from "./components/Blank";

    export default {
        name: 'App',
        components: {
            ColTable,
            RowTable,
            Blank
        },
        data() {
            return {
                isCut: true
            }
        },

        mounted() {

        },

        methods:{
            cut(isCut) {
                this.isCut = isCut
            }
        }

    }
</script>

<style lang="scss">
    *{margin: 0; padding:0; box-sizing: border-box}
    #app {
        width: 100%;
        height: 100vh;
        display: flex;
        .app-left {
            width: 200px;
            height: 100%;
        }
        .app-right {
            flex: 1;
            height: 100%;
        }
    }
</style>
