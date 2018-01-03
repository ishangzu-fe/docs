# 表格字段筛选器

因为业务需要，我们新增了表格字段筛选器，使用非常简单，请参考以下内容。

此组件基于 popup 组件制作。（参见[popup](/popup))

!> tofu >= 0.3.8

## 用法

参考示例：

~~~javascript
<i-field-filter :items="items" @change="handleChange"></i-field-filter>

data () {
    return {
        items: ['a', 'b', 'c']
    }
}

methods: {
    handleChange (selected) {
        // 初始时默认勾选所有字段
        // default return ['a', 'b', 'c']
    }
}
~~~

## Attributes

<table width="100%" cellspacing="0" cellpadding="0" border="1" style="border-collapse: collapse;display: table;text-align: center;">
	<thead>
		<tr>
			<th>参数</th>
			<th>说明</th>
			<th>类型</th>
			<th>可选值</th>
			<th>默认值</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>items</td>
			<td>需要筛选的字段数组</td>
			<td>array</td>
			<td>——</td>
			<td>——</td>
		</tr>
	</tbody>
</table>

## Events

<table width="100%" cellspacing="0" cellpadding="0" border="1" style="border-collapse: collapse;display: table;text-align: center;">
	<thead>
		<tr>
			<th>事件</th>
			<th>说明</th>
			<th>回调参数</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>change</td>
			<td>当选中的字段值发生变化时触发的事件</td>
			<td>选中的字段数组</td>
		</tr>
	</tbody>
</table>
