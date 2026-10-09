---
tags:
  - TinperNext
  - modal组件
---
# 模态框 Modal

## 登陆的模态框

```tsx
import {Button, Checkbox, Form, Icon, Input, Modal} from '@tinper/next-ui';
import React, {ChangeEvent, Component, CompositionEvent, MouseEvent} from 'react';

const FormItem = Form.Item;
interface DemoState {
    showModal?: boolean,
    pawd?: string,
    name?: string,
    showPassword?: boolean}
class Demo2 extends Component<{}, DemoState> {
    constructor(props: {}) {
        super(props);
        this.state = {
            showModal: false,
            pawd: '',
            name: '',
            showPassword: false
        };
        this.close = this.close.bind(this);
        this.open = this.open.bind(this);
    }

    close() {
        this.setState({
            showModal: false
        });
    }

    open() {
        this.setState({
            showModal: true
        });
    }

	handleChange = (state: string, value: ChangeEvent<HTMLInputElement> | MouseEvent<HTMLElement> | CompositionEvent<HTMLElement> | string | number) => {
	    this.setState({
	        [state]: value
	    })
	}

	handleChangeShowPassword = () => {
	    const {showPassword} = this.state
	    this.setState({
	        showPassword: !showPassword
	    })
	}

	render() {
	    const {showPassword} = this.state
	    return (
	        <div className="demo-margin">
	            <Button
	                bordered
	                onClick={this.open}>
					登陆模态框
	            </Button>
	            <Modal
	                visible={this.state.showModal}
	                className="register-demo-modal"
	                onCancel={this.close}
	                height={300}
	                width={320}
	                footer={null}
	            >
	                <Modal.Header closeButton>
	                    <Modal.Title>登陆</Modal.Title>
	                </Modal.Header>

	                <Modal.Body>
	                    <Form>
	                        <FormItem>
	                            <Input
	                                placeholder="手机号/邮箱/用友云账号"
	                                value={this.state.name}
	                                autoComplete="on"
	                                onChange={(value: ChangeEvent<HTMLInputElement> | MouseEvent<HTMLElement> | CompositionEvent<HTMLElement> | string | number, _event?: ChangeEvent<HTMLInputElement> | MouseEvent<HTMLElement> | CompositionEvent<HTMLElement>) => this.handleChange('name', value) }
	                            />
	                        </FormItem>
	                        <FormItem>
	                            <Input
	                                type={showPassword ? "text" : "password"}
	                                placeholder="密码"
	                                autoComplete="new-password"
	                                value={this.state.pawd}
	                                onChange={(value: ChangeEvent<HTMLInputElement> | MouseEvent<HTMLElement> | CompositionEvent<HTMLElement> | string | number, _event?: ChangeEvent<HTMLInputElement> | MouseEvent<HTMLElement> | CompositionEvent<HTMLElement>) => this.handleChange('pawd', value) }

	                                suffix={<Icon style={{fontSize: 12, cursor: 'pointer', color: '#979797'}}
												  onClick={this.handleChangeShowPassword}
												  type={showPassword ? "uf-eye" : "uf-eye-o"}/>}
	                            />
	                        </FormItem>
	                        <FormItem className="u-form-item-custom">
	                            <Checkbox>记住账号</Checkbox>
	                            <Button type="text">忘记密码？</Button>
	                        </FormItem>
	                        <div className="operations">
	                            <Button onClick={this.close} colors="primary">确定</Button>
	                        </div>
	                    </Form>


	                </Modal.Body>
	            </Modal>

	        </div>
	    )
	}
}


export default Demo2;
```

```css
.register-demo-modal {
  .wui-modal-header {
    padding-left: 13px;
  }

  .wui-modal-header,
  .wui-modal-footer {
    border: 0;
  }

  .wui-modal-body {
    padding: 22px 24px 16px 20px;

    .wui-form-item {
      min-height: 44px;
      padding: 0;

      .wui-form-item-control {
        width: 100%;
      }

      &.wui-form-item-custom {
        min-height: 42px;

        .wui-form-item-control-input-content {
          display: flex;
          align-items: center;
          justify-content: space-between;

          .wui-checkbox {
            margin-bottom: -3px;

            .wui-checkbox-label {
              color: #ccc;
            }
          }

          .wui-button-text {
            margin-right: -17px;
          }
        }
      }

      a {
        float: right;
        outline: none;
        text-decoration: none;
      }
    }

    .operations {
      .wui-button {
        display: block;
        width: 100%;
      }
    }
  }
}
```
