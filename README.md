# 大数据精度问题  
前言：在ES6以前，Javascript没有专门的整数类型，所有的数字都被表示为双精度64位浮点数，这就意味着Javascript能安全地处理的整数范围是有限的，超过16位数的大数字会失去精度。

场景：API返回数据：obj_id为18位长度的字符串   https://juejin.cn/post/7348712837849284644

![image](https://github.com/Lujinghui1234/Coding-Common-Error/assets/109168485/d08c40e2-15de-4fb3-ba48-6a3f01b1e967)

问题：使用JSON.parse（obj_id）,变成了898186844400803800，失去了精度。

解决：判断数据类型，如果是大精度数据，就不要JSON.parse()了（这个方法会变成Number,大数据会丢失精度）。
```
if(typeof obj_id === 'string' && /^\d{16,}$/.test(obj_id)){
    return obj_id;
}else{
    return JSON.parse(obj_id)
};
```
# 下拉框全选/全不选
需求是下拉框全选/全不选，点开select，option底部固定了全选和全不选按钮，项目组件库使用material ui V5，如何实现？

解决：使用material中的AutoComplete组件，通过PaperComponent属性传入button，PaperComponent是个自定义渲染button的组件

使用组件：

![image](https://github.com/Lujinghui1234/Coding-Difffculties/assets/109168485/87faa35b-beea-416e-a9c4-d76b9635a3fb)


封装组件：

![image](https://github.com/Lujinghui1234/Coding-Difffculties/assets/109168485/6b2d67fe-5319-4476-9ee7-098ccc7f596d)

![image](https://github.com/Lujinghui1234/Coding-Difffculties/assets/109168485/5aee9007-5245-4d61-99a8-f99ef17c0369)
![image](https://github.com/Lujinghui1234/Coding-Difffculties/assets/109168485/c4499e72-de97-4936-b6c1-2d21c4f3d0cb)
![image](https://github.com/Lujinghui1234/Coding-Difffculties/assets/109168485/7222196c-0c97-4acc-b1c1-88db0a6ef3e7)

# Vue2动态显示隐藏tab组件
需求：两个父组件复用一个tabs组件，其中父组件a有4个tab，父组件b只有3个tab，如何封装tabs组件动态显示/隐藏多出来的那个tab, tab内容较为复杂，不是简单的文本
```
tabs子组件做的事：
1，接受props参数：isNeedFourTab，父组件a、b根据自身需要传递布尔值
props: ['isNeedFourTab']
2，data中定义tabs数组，数组选项中visible变量存储props：isNeedFourTab，用来控制显示/隐藏；activeName动态显示激活的tab
data: {
    activeName: this.isNeedFourTab ? '任务信息' : '检查项',
    tabs: [
        { name: '任务信息', label: '任务信息', visible: this.isNeedFourTab }, //动态显示
        { name: '检查项', label: '检查项', visible: true }, //父组件a、b都显示
        { name: '实施计划', label: '实施计划', visible: true }, //父组件a、b都显示
        { name: '附件列表', label: '附件列表', visible: true } //父组件a、b都显示
    ]
}
3，定义computed计算属性：visibleTabs，过滤得到visible为true的tabs（使用计算属性是因为模板中不允许对data数据同时操作v-if和v-for，影响性能）
computed: {
		visibleTabs() {
			return this.tabs.filter((tab) => tab.visible);
		}
}
4，template模板中v-for遍历visibleTabs，通过v-if判断name，插入插槽template，插槽中书写tab内容
<el-tabs v-model="activeName">
    <el-tab-pane v-for="(item) in visibleTabs" :key="item.name" :label="item.label" :name="item.name">
	<template v-if="item.name==='任务信息' && item.visible">
	<!-- 渲染内容 -->
	</template>
	<template v-else-if="item.name==='检查项'">
	<!-- 渲染内容 -->
	</template>
    </el-tab-pane>
</el-tabs>

```
# Vue2中Form动态切换字段，无法及时收集Table值的问题
```
1，场景：vue2中使用element-ui，上面是form下面是table，form中a字段收集table中b字段的值总和，form中c字段切换值的时候，table表头动态显示，b字段变成了一个新的d字段，由form中的e字段收集
2，问题：切换form中c字段的时候，table表头动态显示，form的a和e字段值无法及时收集并回显
3，解决：
```
# Vue2中弹窗组件复用，无法准确收集值的问题
```
1，场景：某个弹窗组件使用el-tree组件，被复用2次，分别收集字段a和b的值，他们用的是同一个接口查询。第一次打开弹窗收集字段a，第二次打开收集字段b
2，问题：第二次打开时，el-tree收集到的还是第一次的值
3，解决：
```






