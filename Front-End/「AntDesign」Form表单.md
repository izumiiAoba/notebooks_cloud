1. [Ant Design - Form](https://ant.design/components/form-cn/#components-form-demo-validate-other)
2. [Form表单(一) - 掘金](https://juejin.im/post/5c01e96a51882526f96b498a)
3. [Form表单(二) - 掘金](https://juejin.im/post/5c01e97ce51d45225000f34b)
4. [10分钟精通Ant Design Form表单 - 掘金](https://juejin.im/post/5c47ffff51882533e05ef4f9)

***

### 创建实例

- `Form.create`
- 实例提供一系列的方法，如注册、收集、校验
- 包装组件是为了更新组件
- 所有需要该实例进行收集校验的组件，必须要通过`getFieldDecorator`进行修饰(该组件的值将完全由该实例管理)

### 注册

- `getFieldDecorator(id,options)`
- options 是个对象
- 把需要收集的数据在实例中进行注册，并把注册的值同步到被 getFieldDecorator 修饰的组件上
- 组件不能够在通过value赋值，组件的状态将全部由 getFieldDecorator 托管

### 收集

### 校验

***

### options.initialValue

- 初次加载时给默认值应使用 options 中的`initialValue`，而不是在 componentWillMount 中使用 `setFieldsValue()`

### options.getValueFromEvent

- 可以把`onChange`的参数（如 event）转化为控件的值
- 即：将一个函数指定给此属性，函数的返回值作为当前 field 的 value

***

### Tips

#### FormItem 里的嵌套复合组件

使用 getFieldDecorator 注册的时候不应该将整个嵌套的组件注册，只注册其中控制 Field 取值的组件。

以此避免`resetFields()`方法的失效和其他问题。

```jsx
<FormItem
    {...WtFormLayout.formItemLayout}
    label={<span>样本名称<WtHelpTooltip title="用户命名或者条形码" /></span>}
>
    <div style={{ position: 'relative' }}>
        {this.tipSrcCode()}
        {getFieldDecorator('srcCode', srcCodeOption)(
            <Input
                onBlur={e => this.checkSrcCode(e.target.value)}
                onChange={e => this.setSrcCodeValue(e.target.value)}
            />
        )}
    </div>
</FormItem>
```

#### 自定义组件的注册与传值

- `options.valuePropName`：设置在子组件中由 props 接收到的值
- `this.props.onChange`：子组件中使用 props 传入的 onChange 函数，将此注册的子组件的value传给Form表单