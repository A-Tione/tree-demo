<template>
    <div class="content">
        <header class="relative">
            <p>线路选择</p>
            <el-button class="button" type="info" @click="circuitCut" circle></el-button>
            <pop-up class="absolute" :list="list" v-if="visible"></pop-up>
        </header>
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
    </div>
</template>

<script>
    import PopUp from "./PopUp";
    export default {
        name: 'ColTable',
        components: {PopUp},
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
                visible: false,
                filterText: '',
                checkedKeys: [],
                defaultProps: {
                    children: 'children',
                    label: 'label'
                },
                list: [
                    {img:'src/img/基础应用@2.jpg', name: '系统管理'},
                    {img:'src/img/基础应用@2.jpg', name: '系统管理'},
                    {img:'src/img/基础应用@2.jpg', name: '系统管理'},
                    {img:'src/img/基础应用@2.jpg', name: '系统管理'},
                    {img:'src/img/基础应用@2.jpg', name: '系统管理'},
                    {img:'src/img/基础应用@2.jpg', name: '系统管理'},
                    {img:'src/img/基础应用@2.jpg', name: '系统管理'},
                    {img:'src/img/基础应用@2.jpg', name: '系统管理'},
                ]
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
                this.visible = true
                // this.$emit('colCut', false)
            }
        }
    }


</script>

<style lang="scss" scoped>
    @import "src/assets/styles/_variables";

    .content {
        font-size: 12px;
        display: flex;
        flex-direction: column;
        height: 100%;
        padding: 16px 12px;
        header {
            @include flex-vertical-between;
            margin-bottom: 12px;
            position: relative;
            .absolute {
                position: absolute;
                top: 0;
                left: 100%;
                z-index: 1;
            }
            p {
                color: $black;
                font-weight: 600;
            }
            .button{
                position: relative;
                padding: 0;
                width: 14px;
                height: 10px;
                border: 1px solid $black;
                background: white;
                border-radius: 0;
                &::before {
                    position: absolute;
                    content: '';
                    width: 14px;
                    height: 2px;
                    top: -2px;
                    left: -1px;
                    background: $black;
                }
                &::after {
                    position: absolute;
                    content: '';
                    width: 14px;
                    height: 1px;
                    top: -4px;
                    left: -1px;
                    background: $black;
                }
            }
        }
    }
</style>