# JavaMap转Json

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2018-8-14      高天阳	初始化文档

```

## 1 问题描述

在前后端交互中，后台可能由于某种原因，会返回map类型的数据，因此，前端的开发中，需要解析成标准的JSON的格式来使用

### 1.1 解决方案

> 公共方法js

```
const commonApi = {};
/**
 * map转json通用方法
 * @param map
 */
commonApi.mapToJson= function(map){
    var mapData = '';
    var mapDataBak = '';
    var data = [];
    /**
     * 测试数据开始
     */
    // var DATA = [
    //     '[{forPI=91.67, realRepayDate=2017-12-19, id=4}]',
    //     '[{forPI=91.67, realRepayDate=2017-12-19, id=4},{forPI=81.88, realRepayDate=2018-12-18, id=3}]',
    //     '[{forPI=91.67, realRepayDate=2017-12-19, id=4}, {forPI=81.88, realRepayDate=2018-12-18, id=3}]',
    //     '{forPI=91.67, realRepayDate=2017-12-19, id=4}',
    //     '[{forPI=91.67, realRepayDate=2017-12-19, id=4, nameData=[{name=jack},{name=tom}]}]',
    //     '[{forPI=91.67, realRepayDate=2017-12-19, id=4, nameData=[{name=jack},{name=tom}]}, {forPI=81.88, realRepayDate=2018-12-18, id=3, nameData=[{name=mark},{name=lara}]}]',
    //     '{forPI=91.67, realRepayDate=2017-12-19, id=4, nameData=[{name=jack},{name=tom}]}'
    // ];
    // map=DATA[0];
    /**
     * 测试数据结束
     */
    if(map.match(/^\[[\s\S]*\]$/)&&map.match(/^\[[\s\S]*\]$/).index===0&&map.match(/^\[[\s\S]*\]$/).length===1){
        if(map.match(/\[[\s\S]*\[/)&&map.match(/\[[\s\S]*\[/).length>=1){
            console.error('javaMap存在"[[]]"嵌套，无法使用此方法转json！');
            return
        }
        mapData = map;
        if(map.match(/}, {/)&&map.match(/}, {/).length){
            /**
             * 去除'[]' 并按'}, {'分割
             * @type {string[]}
             */
            mapDataBak = mapData.replace(/[\[\]]/g,"").split("}, {");
        }else if(map.match(/},{/)&&map.match(/},{/).length){
            mapDataBak = mapData.replace(/[\[\]]/g,"").split("},{");
        }else{
            mapDataBak = [mapData.replace(/[\[\]]/g,"")];
        }
        _.each(mapDataBak,function (v,k) {
            if(mapDataBak.length===1){
                return
            }
            else if(k===0){
                mapDataBak[k] = v + '}';
            }else if(k===mapDataBak.length-1){
                mapDataBak[k] = '{' + v;
            }else{
                mapDataBak[k] = '{' + v + '}';
            }
        });
        _.each(mapDataBak,function (v) {
            data.push(commonApi.formatJsonMap(v));
        });
        return data;
    }else if(map.match(/^\{[\s\S]*\}$/)&&map.match(/^\{[\s\S]*\}$/).index===0&&map.match(/^\{[\s\S]*\}$/).length===1){
        if(map.match(/\[[\s\S]*\]/)&&map.match(/\[[\s\S]*\]/).length>=1){
            console.error('javaMap存在"{[]}"嵌套，无法使用此方法转json！');
            return
        }
        mapData = map;
        mapDataBak = mapData;
        data.push(commonApi.formatJsonMap(map));
        return data;
    }else{
        console.error('javaMap结构异常，无法使用此方法转json！');
    }
};

commonApi.formatJsonMap = function(obj){
    /**
     * 分析：将字符串中的{}去除，变成基本的字符串，然后使用正则的方法将map转成标准的json个数
     * \s匹配任何不可见字符，包括空格、制表符、换页符等等。等价于[ \f\n\r\t\v]
     * @type {{}}
     */
    var json={};
    var newObj= obj.substring(1,obj.length-1);
    var reg = /([^,\s]+)=([^,\s]+)/g;               //等号的两边是：非，\s的多个字符
    newObj.replace(reg,function(arg0,arg1,arg2){    // arg1第一个分组，arg2第二个分组
        json[arg1] = arg2
    });
    return json;
};
```

> 调用方法页面

```
<script type="text/javascript" src="XX/XX/commonApi.js"></script>
<script>
    console.log(commonApi.mapToJson('${pageBean.page}'));
</script>
```

* `${pageBean.page}`为javaMap

## 参考资料

* [后台返回的map转成json的形式](https://blog.csdn.net/qinchaidaren/article/details/78140914?locationNum=9&fps=1)