<template>
  <!--是否行内表单-->
  <el-form :inline="inline" :model="form" ref="form" label-width="100px">
    <!--标签显示名称-->
    <el-form-item
      v-for="item in formLabel"
      :key="item.model"
      :label="item.label"
    >
      <!--根据type来显示是什么标签-->
      <el-input
        v-model="form[item.model]"
        :placeholder="'请输入' + item.label"
        v-if="item.type === 'input'"
      ></el-input>
      <el-select
        v-model="form[item.model]"
        placeholder="请选择"
        v-if="item.type === 'select'"
      >
        <!--如果是select或者checkbox 、Radio就还需要选项信息-->
        <el-option
          v-for="item in item.opts"
          :key="item.value"
          :label="item.label"
          :value="item.value"
        ></el-option>
      </el-select>
      <el-switch
        v-model="form[item.model]"
        v-if="item.type === 'switch'"
      ></el-switch>
      <el-date-picker
        v-model="form[item.model]"
        type="date"
        placeholder="选择日期"
        v-if="item.type === 'date'"
        value-format="yyyy-MM-dd"
      >
      </el-date-picker>
    </el-form-item>
    <!--留一个插槽-->
    <el-form-item><slot></slot></el-form-item>
  </el-form>
</template>

<script>
export default {
  //inline 属性可以让表单域变为行内的表单域
  //form 表单数据 formLabel 是标签数据
  props: {
    inline: Boolean,
    form: Object,
    formLabel: Array,
  },
  name:'testForm',
  data(){
    return{}
  }
};
</script>