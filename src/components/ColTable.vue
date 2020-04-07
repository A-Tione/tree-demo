<template>
    <div class="content">
        <header>
            <p>线路选择</p>
            <button @click="circuitCut">X</button>
        </header>
        <el-tree
                ref="vueTree"
                node-key="id"
                :data="trees"
                :props="defaultProps"
                :default-expanded-keys="checkedKeys"
                :default-checked-keys="checkedKeys"
                accordion
                highlight-current
                @node-click="handleNodeClick">
        </el-tree>

    </div>
</template>

<script>
    export default {
        name: 'ColTable',

        props: {
            trees: {
                type: Array,
                default() {
                    return []
                }
            },
            idKey: {
                type: Number,
                default() {
                    return 0
                }
            }
        },

        data() {
            return {
                checkedKeys: [],
                defaultProps: {
                    children: 'children',
                    label: 'label'
                }
            }

        },
        computed: {},

        watch: {
            idKey() {
                this.updateInfo()
            }
        },

        mounted() {
            this.updateInfo()
        },

        methods: {
            updateInfo() {
                this.$refs.vueTree.setCurrentKey(this.idKey)
                this.checkedKeys = [this.idKey]
            },
            handleNodeClick(node) {
                this.$emit('updateIdKey', node.id)
            },
            circuitCut() {
                this.$emit('colCut', false)
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

            button {
                width: 20px;
                height: 20px;
                cursor: pointer;
            }
        }
    }
</style>