<template>
    <div class="content">
        <header>
            <p>线路选择</p>
            <button @click="circuitCut">X</button>
        </header>
        <el-tree
                :data="data"
                :props="defaultProps"
                accordion
                @node-click="handleNodeClick">
        </el-tree>

    </div>
</template>

<script>
    export default {
        name: "ColTable",

        data() {
            return {
                data: [{
                    id: 1,
                    label: '一级 1',
                    children: [{
                        id: 4,
                        label: '二级 1-1',
                        children: [{
                            id: 9,
                            label: '三级 1-1-1'
                        }, {
                            id: 10,
                            label: '三级 1-1-2'
                        }]
                    }]
                }, {
                    id: 2,
                    label: '一级 2',
                    children: [{
                        id: 5,
                        label: '二级 2-1'
                    }, {
                        id: 6,
                        label: '二级 2-2'
                    }]
                }, {
                    id: 3,
                    label: '一级 3',
                    children: [{
                        id: 7,
                        label: '二级 3-1'
                    }, {
                        id: 8,
                        label: '二级 3-2'
                    }]
                }],
                defaultProps: {
                    children: 'children',
                    label: 'label'
                }
            };

        },

        props: {},

        mounted() {
        },

        methods: {
            circuitCut() {
                this.$emit('colCut', false)
            },
            handleNodeClick(data) {
                console.log(data);
            }
        }
    }


</script>

<style lang="scss" scoped>
    .content {
        display: flex;
        flex-direction: column;
        background: orange;
        height: 100%;
        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            button{
                width: 20px;
                height: 20px;
                cursor: pointer;
            }
        }
    }
</style>