<template>
    <div class="content">
        <div class="left">
            <el-menu class="el-menu-demo" mode="horizontal">
                <el-submenu index="1">
                    <template slot="title">线路选择</template>
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
                        class="tags"
                        :class="{active: clickId === tag.id}"
                        @click="clickTag(tag)"
                        @close="closeTag(tag.id)">
                    {{tag.label}}
                </el-tag>
            </div>
        </div>
        <div class="right">
            <el-button class="button" type="info" @click="circuitCut" circle></el-button>
        </div>
    </div>
</template>

<script>
    export default {
        name: "RowTable",

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

        watch: {
            nodeKeyObj() {
                this.updateInfo()
                this.updateInfoTree()
            }
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
                    if (!index) { //重复tag则不加
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
                    this.$emit('updateIdKey', tag)
                }
            },
            closeTag(id) {
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
        width: 100%;
        height: 48px;
        .left{
            display: flex;
            align-items: center;
            width: 90%;
            .el-menu-demo {
                width: 120px;
                height: 24px;
                margin-right: 20px;
                display: flex;
                align-items: center;
            }
            .tags {
                margin-right: 10px;
                cursor: pointer;
                border: 1px solid rgba(0, 0, 0, 0.15);
                color: rgba(0, 0, 0, 0.65);
                background: white;
                &.active {
                    border: 1px solid #91D5FF;
                    color: #1890FF;
                    background: #E6F7FF;
                }
            }
        }
        .right{
            width: 10%;
            display: flex;
            justify-content: flex-end;
            margin-right: 10px;
            .button {
                position: relative;
                padding: 0;
                width: 10px;
                height: 14px;
                border: 1px solid rgba(0, 0, 0, 0.65);
                background: white;
                border-radius: 0;
                &::before {
                    position: absolute;
                    content: '';
                    width: 2px;
                    height: 14px;
                    top: -1px;
                    left: -2px;
                    background: rgba(0, 0, 0, 0.65);
                }
                &::after {
                    position: absolute;
                    content: '';
                    width: 1px;
                    height: 14px;
                    top: -1px;
                    left: -4px;
                    background: rgba(0, 0, 0, 0.65);
                }
            }
        }

    }
</style>