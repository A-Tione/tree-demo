<template>
    <div class="content">
        <div class="left">
            <el-menu class="el-menu-demo" mode="horizontal">
                <el-submenu index="1">
                    <template slot="title">线路选择</template>
                    <el-input
                            class="el-input-class"
                            placeholder="搜索部门/线路"
                            v-model="filterText">
                        <i slot="prefix" class="el-input__icon el-icon-search"></i>
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
                filterText: '',
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
            },
            filterText(val) {
                this.$refs.vueTree.filter(val);
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
            filterNode(value, data) {
                if (!value) return true;
                return data.label.indexOf(value) !== -1;
            },
            updateInfoTree() {
                if (this.nodeKeyObj && this.nodeKeyObj.id) {
                    this.$refs.vueTree.setCurrentKey(this.nodeKeyObj.id)
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
    @import "src/assets/styles/_variables";

    .content{
        @include flex-vertical-between;
        width: 100%;
        height: 48px;
        .left{
            display: flex;
            align-items: center;
            width: 90%;
            .el-menu-demo {
                width: 120px;
                height: 32px;
                margin-right: 20px;
                display: flex;
                align-items: center;
            }
            .tags {
                margin-right: 10px;
                cursor: pointer;
                border: 1px solid rgba(0, 0, 0, 0.15);
                color: $black;
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
                border: 1px solid $black;
                background: white;
                border-radius: 0;
                &::before {
                    position: absolute;
                    content: '';
                    width: 2px;
                    height: 14px;
                    top: -1px;
                    left: -2px;
                    background: $black;
                }
                &::after {
                    position: absolute;
                    content: '';
                    width: 1px;
                    height: 14px;
                    top: -1px;
                    left: -4px;
                    background: $black;
                }
            }
        }
    }
</style>