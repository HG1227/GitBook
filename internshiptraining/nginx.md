Nginx

1、登录公司服务器

ssh member@haomo-studio.com

![](blob:https://www.gitbook.com/2bc9673d-6384-4623-941a-642015b0d2d4)

2、打开nginx配置文件

vim /etc/nginx/nginx.conf

![](blob:https://www.gitbook.com/62e061d3-b772-4809-a789-97e5819d2051)

3、找到organization对应接口，修改return里的东西

![](blob:https://www.gitbook.com/c948ecb7-30b8-42a1-a1b8-65dbe0db6180)

{

```
"orgName": "生命滙总部",

"orgId": "69EBAE21B3D347ECA09F82A848AE7E4C",

"children": \[

    {

        "orgName": "生命汇上海公司",

        "orgId": "EAF2746C2C444C8B8AFEAA482F5B7164",

        "children": \[\]

    },

    {

        "orgName": "生命滙广州公司",

        "orgId": "FECC04D660E3474FA474CDBA0706F2D1",

        "children": \[\]

    },

    {

        "orgName": "生命滙北京公司",

        "orgId": "280649403EF74F09B583C92E55D7EE45",

        "children": \[

            {

                "orgName": "生命滙北京公司-市场部",

                "orgId": "665630463717408D96AD66C7BE94F7B4",

                "children": \[\]

            }

        \]

    },

    {

        "orgName": "生命滙海南公司",

        "orgId": "8CBBE14B384D4E969105AAB56C5E475B",

        "children": \[\]

    }

\]
```

}

![](blob:https://www.gitbook.com/f12d15ff-b68d-43dc-a77b-78133af2a51e)

4、保存并退出

Ctrl+C:wq

5、启动nginx

sudo gitlab-ctl restart nginx

（公司密码:$ecur1ty@haomo）

