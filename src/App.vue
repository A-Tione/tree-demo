<template>
    <div id="app">
        <div v-if="isCut" class="app-left">
            <col-table :trees="trees"
                       :nodeKeyObj="nodeKeyObj"
                       @updateIdKey="updateIdKey"
                       @colCut="cut">

            </col-table>
        </div>
        <div class="app-right">
            <row-table v-show="!isCut"
                       :trees=trees
                       :nodeKeyObj="nodeKeyObj"
                       @updateIdKey="updateIdKey"
                       @rowCut="cut">

            </row-table>
            <blank></blank>
        </div>
    </div>
</template>


<script>
    import ColTable from './components/ColTable'
    import RowTable from './components/RowTable'
    import Blank from './components/Blank'

    export default {
        name: 'App',

        components: {
            ColTable,
            RowTable,
            Blank
        },

        data() {
            return {
                isCut: true,
                nodeKeyObj: null,
                trees: [{
                    id: 1,
                    label: '长沙众旺公司',
                    children: [{
                        id: 4,
                        label: '第一大队',
                        children: [{
                            id: 9,
                            label: '905路'
                        }, {
                            id: 10,
                            label: '906路'
                        }]
                    }]
                }, {
                    id: 2,
                    label: '益阳众旺公司',
                    children: [{
                        id: 5,
                        label: '第二大队'
                    }, {
                        id: 6,
                        label: '第三大队'
                    }]
                }]
            }
        },

        methods: {
            cut(isCut) {
                this.isCut = isCut
            },
            updateIdKey(nodeKeyObj) {
                this.nodeKeyObj = nodeKeyObj
            }
        }

    }
</script>

<style lang="scss">
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box
    }
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
