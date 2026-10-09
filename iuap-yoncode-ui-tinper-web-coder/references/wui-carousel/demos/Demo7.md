---
tags:
  - TinperNext
  - carousel组件
---
# 走马灯 Carousel

## 垂直轮播

垂直方向滚动

```tsx
import { Carousel } from "@tinper/next-ui";
import React, { Component } from "react";

class Demo7 extends Component {
  beforeChange = (from: number, to: number) => {
      console.log(from, to);
  };

  afterChange = (current: number) => {
      console.log(current);
  };

  render() {
      return (
          <Carousel
              autoplay
              autoplaySpeed={2000}
              speed={2000}
              dots={false}
              vertical={true}
              fieldid="carousel"
              cssEase="linear"
              beforeChange={this.beforeChange}
              afterChange={this.afterChange}
          >
              <div>
                  <h3>1</h3>
              </div>
              <div>
                  <h3>2</h3>
              </div>
              <div>
                  <h3>3</h3>
              </div>
              <div>
                  <h3>4</h3>
              </div>
          </Carousel>
      );
  }
}

export default Demo7;
```
