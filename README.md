# 大数据精度问题
前言：在ES6以前，Javascript没有专门的整数类型，所有的数字都被表示为双精度64位浮点数，这就意味着Javascript能安全地处理的整数范围是有限的，超过16位数的大数字会失去精度。

场景：API返回数据：obj_id为18位长度的字符串

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




