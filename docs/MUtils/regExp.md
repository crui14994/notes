## MUtils.regExp

基于 elementUI 表单封装的正则配置；

#### getElementRules 方法

通过此方法生成 elementUI 表单的验证规则。

```js
let itemConfig = {
  label: "价格",
  prop: "price",
  rules: ["required", "decimal"],
  decimalNumber: 3, //保留3位小数的数字
};
let rule = regExp.getElementRules(itemConfig);
```

###### itemConfig 属性如下:

| 规则名称      | type   | 描述                                            | 默认值 |
| ------------- | ------ | ----------------------------------------------- | ------ |
| label         | String | 表单名称                                        | -      |
| prop          | String | vue 表单需要绑定的属性                          | -      |
| rules         | Array  | 规则列表；具体参考下面的 rules 表格             | -      |
| decimalNumber | Number | 要保留的小数点个数;只对需要填写小数点的表单生效 | 2      |

###### rules 规则列表

| 规则名称      | 描述                              | 默认值 |
| ------------- | --------------------------------- | ------ |
| required      | 是否必填                          | -      |
| integer       | 正负整数(含 0)                    | -      |
| integer2      | 正负整数(不含 0)                  | -      |
| integerPlus   | 正整数(含 0)                      | -      |
| integerPlus2  | 正整数(不含 0)                    | -      |
| integerMinus  | 负整数(含 0)                      | -      |
| integerMinus2 | 负整数(不含 0)                    | -      |
| decimal       | 正负数，最多保留 n 位小数(含 0)   | -      |
| decimal2      | 正负数，最多保留 n 位小数(不含 0) | -      |
| decimalPlus   | 正数，最多保留 n 位小数(含 0)     | -      |
| decimalPlus2  | 正数，最多保留 n 位小数(不含 0)   | -      |
| decimalMinus  | 负数，最多保留 n 位小数(含 0)     | -      |
| decimalMinus2 | 负数，最多保留 n 位小数(不含 0)   | -      |
