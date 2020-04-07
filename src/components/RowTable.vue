<template>
    <div class="content">
        <div class="left">
            <el-menu :default-active="activeIndex" class="el-menu-demo" mode="horizontal" @select="handleSelect">
                <el-submenu index="2">
                    <template slot="title">线路萱蕚</template>
                    <el-menu-item index="2-1">选项1</el-menu-item>
                    <el-menu-item index="2-2">选项2</el-menu-item>
                    <el-menu-item index="2-3">选项3</el-menu-item>
                    <el-submenu index="2-4">
                        <template slot="title">选项4</template>
                        <el-menu-item index="2-4-1">选项1</el-menu-item>
                        <el-menu-item index="2-4-2">选项2</el-menu-item>
                        <el-menu-item index="2-4-3">选项3</el-menu-item>
                    </el-submenu>
                </el-submenu>
            </el-menu>
            <el-tag
                    v-for="tag in dynamicTags"
                    :key="tag"
                    closable
                    :disable-transitions="false"
                    @close="handleClose(tag)">
                    {{tag}}
            </el-tag>
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
                dynamicTags: ['标签一', '标签二', '标签三'],
                activeIndex: '1',
                activeIndex2: '1',
            }
        },

        props:{},

        mounted() {
        },

        methods: {
            circuitCut() {
                this.$emit('rowCut', true)
            },
            handleSelect(key, keyPath) {
                console.log(key, keyPath);
            },
            handleClose(tag) {
                this.dynamicTags.splice(this.dynamicTags.indexOf(tag), 1);
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