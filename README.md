<!--
 * @Author: HaoJie
 * @Date: 2023-01-29 14:27:55
 * @LastEditTime: 2023-01-29 16:45:54
 * @LastEditors: HaoJie
 * @FilePath: \p-element\README.md
-->

# p-element

仿 element 的组件库，使用 vue 来实现

## select 选择器

当选项过多时，使用下拉菜单展示并选择内容。

### Attributes

| 参数        | 说明                    | 类型              | 可选值 | 默认值   |
| ----------- | ----------------------- | ----------------- | ------ | -------- |
| optionList  | 下拉框的数据            | Array[key, value] | -      | []       |
| placeholder | 占位符                  | String            | -      | 请选择   |
| emptyText   | optionList 为空时的文案 | String            | -      | 暂无数据 |
| disabled    | 禁用选择                | Boolean           | -      | false    |

### Events

| 事件名称 | 说明             | 回调参数 |
| -------- | ---------------- | -------- |
| change   | 选择的值发生变化 | value    |
| clear    | 点击清空按钮     | true     |
