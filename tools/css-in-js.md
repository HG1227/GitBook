# css in js

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2018-09-05        高天阳     初始化文档

```

## 简介



## material-ui withStyles的使用

### 实例 

```js
import React from 'react';
import PropTypes from 'prop-types';
import { withStyles } from '@material-ui/styles';
import Button from '@material-ui/core/Button';

const styles = {
  root: {
    background: 'linear-gradient(45deg, #FE6B8B 30%, #FF8E53 90%)',
    border: 0,
    borderRadius: 3,
    boxShadow: '0 3px 5px 2px rgba(255, 105, 135, .3)',
    color: 'white',
    height: 48,
    padding: '0 30px',
    '&:hover': {
      background: 'linear-gradient(45deg, #FF8E53 30%, #FE6B8B 90%)',
    }
  },
};

function HigherOrderComponent(props) {
  const { classes } = props;
  return <Button className={classes.root}>Higher-order component</Button>;
}

HigherOrderComponent.propTypes = {
  classes: PropTypes.object.isRequired,
};

export default withStyles(styles)(HigherOrderComponent);
```

## 参考资料

* [CSS-in-JS，向Web组件化再迈一大步](https://www.jianshu.com/p/cefd3ae73255)
* [Higher-order component API](https://material-ui.com/zh/styles/basics/#higher-order-component-api)
