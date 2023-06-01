> 基于 elementUI 表单封装的正则配置；

#### getElementRules 方法

通过此方法生成 elementUI 表单的验证规则。

```js
let itemConfig = {
  label: "价格",
  prop: "price",
  rules: ["required", "decimal"],
  decimalNumber: 3, //保留3位小数的数字
};
let rule = mUtils.getElementRules(itemConfig);
```

###### itemConfig 属性如下:

| 规则名称      | type   | 描述                                            | 默认值 |
| ------------- | ------ | ----------------------------------------------- | ------ |
| label         | String | 表单名称                                        | -      |
| prop          | String | vue 表单需要绑定的属性                          | -      |
| rules         | Array  | 规则列表；具体参考下面的 rules 表格             | -      |
| decimalNumber | Number | 要保留的小数点个数;只对需要填写小数点的表单生效 | 2      |
| maxLength     | Number | 最大长度;只对 maxLength 规则生效                | 10     |
| minLength     | Number | 最小长度;只对 minLength 规则生效                | 1      |

###### rules 规则列表

| 规则名称      | 描述                              | 默认值 |
| ------------- | --------------------------------- | ------ |
| required      | 是否必填                          | -      |
| maxLength     | 最大长度                          | -      |
| minLength     | 最小长度                          | -      |
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
| Chinese       | 只能输入中文                      | -      |
| English       | 只能输入英文字母                  | -      |

###### 案列：

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <!-- import CSS -->
    <link
      rel="stylesheet"
      href="https://unpkg.com/element-ui/lib/theme-chalk/index.css"
    />
  </head>

  <body>
    <div id="app">
      <div class="reg-box">
        <el-form
          size="mini"
          :model="ruleForm"
          ref="ruleForm"
          label-width="0px"
          class="demo-ruleForm"
        >
          <el-form-item
            class="reg-item"
            v-for="(item,index) in itemArr"
            :key="index"
            label=""
            :prop="item.prop"
            :rules="getRules(item)"
          >
            <p>{{item.label}}</p>
            <el-input v-model="ruleForm[item.prop]"></el-input>
          </el-form-item>

          <el-form-item>
            <el-button type="primary" @click="submitForm('ruleForm')"
              >立即创建</el-button
            >
          </el-form-item>
        </el-form>
      </div>
    </div>
  </body>
  <style>
    * {
      margin: 0;
      padding: 0;
    }

    .reg-box {
      width: 90%;
      margin: 30px auto;
    }
    .demo-ruleForm {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
    }
    .reg-item {
      width: 24%;
    }
  </style>
  <!-- import Vue before Element -->
  <script src="https://unpkg.com/vue@2/dist/vue.js"></script>
  <!-- import JavaScript -->
  <script src="https://unpkg.com/element-ui/lib/index.js"></script>
  <script type="module">
    import mUtils from "../src/index.js";

    new Vue({
      el: "#app",
      data: function () {
        return {
          ruleForm: {},
          itemArr: [
            {
              label: "最长字符",
              prop: "maxLength",
              rules: ["required", "maxLength"],
              maxLength: 3, //最长字符
            },
            {
              label: "最小字符",
              prop: "minLength",
              rules: ["required", "minLength"],
              minLength: 5, //最长字符
            },
            {
              label: "正负整数(含0)",
              prop: "integer",
              rules: ["required", "integer"],
            },
            {
              label: "正负整数(不含0)",
              prop: "integer2",
              rules: ["required", "integer2"],
            },
            {
              label: "正整数(含0)",
              prop: "integerPlus",
              rules: ["required", "integerPlus"],
            },
            {
              label: "正整数(不含0)",
              prop: "integerPlus2",
              rules: ["required", "integerPlus2"],
            },
            {
              label: "负整数(含0)",
              prop: "integerMinus",
              rules: ["required", "integerMinus"],
            },
            {
              label: "负整数(不含0)",
              prop: "integerMinus2",
              rules: ["required", "integerMinus2"],
            },
            {
              label: "正负数，最多保留2位小数(含0)",
              prop: "decimal",
              rules: ["required", "decimal"],
              decimalNumber: 2, //2位小数,不能为0
            },
            {
              label: "正负数，最多保留2位小数(不含0)",
              prop: "decimal2",
              rules: ["required", "decimal2"],
              decimalNumber: 2, //2位小数
            },
            {
              label: "正数，最多保留2位小数(含0)",
              prop: "decimalPlus",
              rules: ["required", "decimalPlus"],
              decimalNumber: 2, //2位小数
            },
            {
              label: "正数，最多保留2位小数(不含0)",
              prop: "decimalPlus2",
              rules: ["required", "decimalPlus2"],
              decimalNumber: 2, //2位小数
            },
            {
              label: "负数，最多保留2位小数(含0)",
              prop: "decimalMinus",
              rules: ["required", "decimalMinus"],
              decimalNumber: 2, //2位小数
            },
            {
              label: "负数，最多保留2位小数(不含0)",
              prop: "decimalMinus2",
              rules: ["required", "decimalMinus2"],
              decimalNumber: 2, //2位小数
            },
            {
              label: "中文",
              prop: "Chinese",
              rules: ["required", "Chinese"],
            },
            {
              label: "英文字母",
              prop: "English",
              rules: ["required", "English"],
            },
          ],
        };
      },
      created() {
        console.log(mUtils);
      },
      computed: {
        getRules() {
          return (item) => {
            return mUtils.getElementRules(item);
          };
        },
      },
      methods: {
        submitForm(formName) {
          this.$refs[formName].validate((valid) => {
            if (valid) {
              // alert('submit!');
            } else {
              console.log("error submit!!");
              return false;
            }
          });
        },
      },
    });
  </script>
</html>
```
