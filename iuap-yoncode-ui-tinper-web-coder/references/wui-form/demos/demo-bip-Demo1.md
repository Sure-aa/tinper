---
tags:
  - TinperNext
  - form组件
---
# 表单 Form

## 单个FormItem布局

使用FormItem

```tsx
import {Form, Input} from '@tinper/next-ui'
import React, {Component} from 'react'

const formItemLayout = {
    labelCol: {
        xs: {span: 4},
        sm: {span: 4}
    },
    wrapperCol: {
        xs: {span: 8},
        sm: {span: 8}
    }
}
const Demo1 = Form.createForm()(
    class Demo extends Component {

        render() {
            return (
                <Form.Item {...formItemLayout} label='姓名' name='name' colon>
                    <Input placeholder='请输入姓名'/>
                </Form.Item>
            )
        }
    }
)

export default Demo1
```

```css
.wui-form.demo1 {
  width: 300px;
}
#Demo6 .wui-upload {
  width: 100%;
  .btnName {
    width: 100%;
  }
}

.form-other-demo2 {
  .form-item-style {
    .wui-form-item-label {
      width: 16.6666666667%;
    }
    .wui-form-item-control {
      width: 33.3333333333%;
    }
  }
  .form-item-inline-before {
    width: 32.4%;
    .wui-form-item-label {
      width: 51.428%;
    }
    .wui-form-item-control {
      width: 48.572%;
    }
  }
  .form-item-inline-after {
    width: 17.6%;
    .wui-form-item-label {
      padding: 0 3px;
    }
    .wui-form-item-control {
      width: calc(100% - 16px);
    }
  }
}
```
