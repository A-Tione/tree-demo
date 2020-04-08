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
            nodeKeyObj: {
                type: Object,
                default() {
                    return {}
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
                if (this.nodeKeyObj && this.nodeKeyObj.id) {
                    this.$refs.vueTree.setCurrentKey(this.nodeKeyObj.id)
                    this.checkedKeys = [this.nodeKeyObj.id]
                }
            },
            handleNodeClick(nodeKeyObj) {
                if (!nodeKeyObj.children) {
                    this.$emit('updateIdKey', nodeKeyObj)
                }
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