<template>
    <div class="content">
        <header>
            <p>线路选择</p>
            <el-button class="button" type="info" @click="circuitCut" circle>  </el-button>
        </header>
        <el-input
                class="input-class"
                placeholder="搜索部门/线路"
                v-model="filterText">
        </el-input>
        <el-tree
                ref="vueTree"
                node-key="id"
                :data="trees"
                :props="defaultProps"
                :default-expanded-keys="checkedKeys"
                :default-checked-keys="checkedKeys"
                :filter-node-method="filterNode"
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
                filterText: '',
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
            },
            filterText(val) {
                this.$refs.vueTree.filter(val);
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
            filterNode(value, data) {
                if (!value) return true;
                return data.label.indexOf(value) !== -1;
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
        font-size: 12px;
        display: flex;
        flex-direction: column;
        height: 100%;
        padding: 16px 12px;
        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 12px;
            p {
                color: rgba(0, 0, 0, 0.85);
                font-weight: 600;
            }
            .button{
                position: relative;
                padding: 0;
                width: 14px;
                height: 10px;
                border: 1px solid rgba(0, 0, 0, 0.65);
                background: white;
                border-radius: 0;
                &::before {
                    position: absolute;
                    content: '';
                    width: 14px;
                    height: 2px;
                    top: -2px;
                    left: -1px;
                    background: rgba(0, 0, 0, 0.65);
                }
                &::after {
                    position: absolute;
                    content: '';
                    width: 14px;
                    height: 1px;
                    top: -4px;
                    left: -1px;
                    background: rgba(0, 0, 0, 0.65);
                }
            }
        }
        .input-class {
            margin-bottom: 12px;
        }
    }
</style>