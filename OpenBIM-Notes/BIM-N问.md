

#  1 BIM数据和传统三维数据的区别是什么

传统三维：更注重模型形状（建模技术）、外观（怎么变得好看，涉及设计、贴图、材质、渲染、烘培、打光等操作）

BIM：弱化外观，虽然也可以弄得好看（但不是主业）。BIM数据除了记载几何形状，还强调建筑信息在模型中的复杂关系，强调建筑信息所能创造的价值。

# 2 BIM的概念从何而来

工地。现代化工地。是一种三维的 CAD。

# 3 BIM有哪些数据格式

.ifc（开源标杆，文本文件，用 `express` 语言记录数据）

.rvt（商业标杆，二进制）

.xdb（国内小众，sqlite改，未大规模公开使用）

# 4 BIM有规范吗

从数据标注来看，国际通用 ifc

从各地区、各国家因地制宜的生产规范来看，没有统一规范，各搞各的

# 5 BIM解决了什么问题 如何解决的

就像当年 AutoCAD 解决了平面图纸绘制的问题一样。。。

BIM软件首先解决了三维图纸绘制、复杂信息存储，二维做不到的空间之间的关系，在三维解决了。

在生产运用方面，有可视化的bim软件辅助建设，可以精细化设计、建造，甚至是建成后的管理仍旧可以继续使用bim软件。

# 6 BIM数据和几大渲染格式如何转换

rvt导出：只能是开源格式，例如 obj/fbx/gltf 等，才能进行下一步

ifc：与rvt同理

转换的关键有3处：bim的结构信息如何无损转换，bim的三维数据（代表几何形状的顶点和代表外观的材质纹理贴图）如何无损转换，bim数据如何无损地转换。

# 7 我国BIM现状

鱼龙混杂。