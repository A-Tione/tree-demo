<template>
    <div class="content">
        <div class="left">
            <el-menu class="el-menu-demo" mode="horizontal">
                <el-submenu index="1">
                    <template slot="title">线路查询</template>
                    <el-tree
                            ref="vueTree2"
                            node-key="id"
                            :data="trees"
                            :props="defaultProps"
                            :default-expanded-keys="checkedKeys"
                            :default-checked-keys="checkedKeys"
                            accordion
                            highlight-current
                            @node-click="handleNodeClick">
                    </el-tree>
                </el-submenu>
            </el-menu>
            <div v-if="dynamicTags">
                <el-tag
                        v-for="tag in dynamicTags"
                        :key="tag.id"
                        closable
                        :disable-transitions="false"
                        :class="{active: clickId === tag.id}"
                        @click="clickTag(tag)"
                        @close="handleClose(tag.id)">
                    {{tag.label}}
                </el-tag>
            </div>
        </div>
        <div class="right">
            <button @click="circuitCut">X</button>
        </div>
    </div>
</template>

<script>
    export default {
        name: "RowTable",
        data() {
            return {
                clickId: 0,
                dynamicTags: [],
                checkedKeys: [],
                defaultProps: {
                    children: 'children',
                    label: 'label'
                }
            }
        },

        props:{
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

        watch: {
            nodeKeyObj() {
                this.updateInfo()
                this.updateInfoTree()
            }
        },

        mounted() {
            this.updateInfo()
            this.updateInfoTree()
        },

        methods: {
            updateInfo() {
                let index
                if (this.nodeKeyObj && this.nodeKeyObj.id) {
                    for (let i=0; i<this.dynamicTags.length; i++) {
                        if(this.dynamicTags[i].id === this.nodeKeyObj.id) {
                            index = 1
                        }
                    }
                    if (!index) {
                        this.dynamicTags.unshift(this.nodeKeyObj)
                    }
                    this.clickId = this.nodeKeyObj.id
                }
            },
            updateInfoTree() {
                if (this.nodeKeyObj && this.nodeKeyObj.id) {
                    this.$refs.vueTree2.setCurrentKey(this.nodeKeyObj.id)
                    this.checkedKeys = [this.nodeKeyObj.id]
                }
            },
            circuitCut() {
                this.$emit('rowCut', true)
            },
            handleNodeClick(nodeKeyObj) {
                if (!nodeKeyObj.children) {
                    this.$emit('updateIdKey', nodeKeyObj)
                }
            },
            clickTag(tag) {
                if (this.clickId) {
                    this.clickId = tag.id
                    console.log(tag)
                    this.$emit('updateIdKey', tag)
                }
            },
            handleClose(id) {
                let index
                for (let i=0; i<this.dynamicTags.length; i++) {
                    if (this.dynamicTags[i].id === id) {
                        index = i
                        break
                    }
                }
                this.dynamicTags.splice(index, 1)
            },

        }
    }
</script>

<style lang="scss" scoped>
    .content{
        display: flex;
        justify-content: space-between;
        align-items: center;
        background: #42b983;
        width: 100%;
        height: 100px;
        .left{
            .el-menu-demo {
                width: 120px;
                margin-right: 20px;
            }
            width: 90%;
            p {
                margin: 10px;
            }
            display: flex;
            align-items: center;
            .active {
                background: orangered;
            }
        }
        .right{
            width: 10%;
            display: flex;
            justify-content: flex-end;
            margin-right: 10px;
            button{
                width: 20px;
                height: 20px;
                cursor: pointer;
            }
        }

    }
</style>