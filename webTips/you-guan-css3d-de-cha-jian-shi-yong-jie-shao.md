# css3d-插件

css 3d引擎，为方便工作需要制作  
优势:因为是基于div+css3实现,相对canvas webgl拥有更好的平台兼容性。  
劣势:渲染性能相比canvas webgl要弱,只适合创建较小的三维面片场景。  
但是只有14k,相比那些动辄300-400k的大型3d库,这是个非常小巧实用的辅助支持库。

注意1:为了节约计算量,transform部分没有使用matrix,只用了最基本的translate,rotation,scale等属性的排列,默认的旋转顺序是  
rotationX\(\),rotationY\(\),rotationZ\(\),这样无法解决万向锁等问题,所以在使用时需要了解适应这点。如果需要调整可以使用sort\(\)命令调整旋转顺序。

注意2:旧版的Cube更新为Box

## 链接地址

[https://github.com/shrekshrek/css3d-engine](https://github.com/shrekshrek/css3d-engine)

