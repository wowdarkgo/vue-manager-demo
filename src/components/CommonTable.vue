<template>
    <div class="common-table">
        <!--stripe斑马纹  v-loading用来加动画-->
        <el-table :data="tableData" height="590px" stripe v-loading="config.loading" max-height="100%">
            <!-- 第一行序号 -->
            <el-table-column label="序号" width="85">
                <!--slot-scope="scope" 这里取到当前单元格,scope.$index就是索引 默认从0开始这里从1开始-->
                <template slot-scope="scope">
                    <span style="margin-left: 10px">{{ (config.page - 1) * 20 + scope.$index + 1 }}</span>
                </template>
            </el-table-column>
            <!--show-overflow-tooltip 当内容过长被隐藏时显示 tooltip-->
            <el-table-column show-overflow-tooltip v-for="item in tableLabel" :key="item.prop" :label="item.label" :width="item.width ? item.width : 125">
                <!--其实可以在上面:prop="item.prop"就可以显示表单数据 这里设置插槽的方式话更加灵活 我们可以写样式-->
                <template slot-scope="scope">
                    <span style="margin-left: 10px">{{ scope.row[item.prop] }}</span>
                </template>
            </el-table-column>
            <!--操作-->
            <el-table-column label="操作" min-width="180">
                <template slot-scope="scope">
                    <el-button size="min" @click="handleEdit(scope.row)">编辑</el-button>
                    <el-button size="min" type="danger" @click="handleDelete(scope.row)">删除</el-button>
                </template>
            </el-table-column>
        </el-table>
        <!--分页-->
        <el-pagination class="pager" layout="prev, pager, next" :total="config.total"  background :current-page.sync="config.page" @current-change="changePage" :page-size="20"></el-pagination>
    </div>
</template>

<script>
    // config分页数据，这里面至少包括当前页码 总数量
    export default {
        props: {
            tableData: Array,
            tableLabel: Array,
            config: Object
        },
        methods: {
            //更新
            handleEdit(row) {
                this.$emit('edit', row)
            },
            //删除
            handleDelete(row) {
                this.$emit('del', row)
            },
            //分页
            changePage(page) {
                this.$emit('changePage', page)
            }
        }
    }
</script>