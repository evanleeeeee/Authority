# 权限模块需求文档
## 0.文档描述
| 修订时间 | 修订内容 |修订人 | 备注 |
| --- | --- |--- | --- |
| 2018-11-19 | 文档创建 | 李一凡 | |
| 2018-11-23 | 文档添加多条规则 | 李一凡 | 添加内容可见性范围的相关规则 |
| 2018-11-28 | 文档添加如何在后台内容模块添加可见性设置的示例 | 李一凡 | 新增两页页面介绍 |

## 1.规则说明
### 1.1 角色
* 超级管理员
  > 能够访问整个系统的用户。默认情况下，有一个超级管理员账户。该账户用来进行系统的初始配置，用于添加首批的业务人员和配置基本的角色。该角色在系统中为隐形的状态。

* 默认角色
  > 给自行加入系统的用户自动分配的角色，该角色无法访问系统任何数据。管理员给该用户分配其他角色之后，自动取消该用户的初始角色。

* 其他角色
  > 根据企业需求，自定义的角色。

* 角色关联
  > 每个人都能关联一个或多个角色，关联多个角色之后，该人员拥有所有角色权限之和。

### 1.2 权限
* 具体权限参考2.2权限表

* 操作权限
  > 能做什么，如发布课程。

* 数据权限
  > 能操作哪些数据，如只能查看本人发布的课程。

* 内容可见性
  > 管理员上传的内容可以给哪些部门看到。

* 查看权限优先于增删改权限
  > 配置其他权限时，默认赋予查看权限；取消查看权限时，默认取消其他权限。

### 1.3 规则
* 超级管理员拥有最大权限
  > 系统中的超级管理员可以增删改查系统中所有部门，所有管理员的数据。

* 普通管理员用户在自己的数据权限范围内，可以对自己的数据拥有增删改查的权限
  > 例：如下图所示，假设B拥有部门1和部门2的数据权限，则B可以对b1和c1发布任务。且B对该任务拥有所有操作权限。<br>![avatar](../Authority/img/rule01.png)

* 普通管理员用户在自己拥有的数据权限范围内，只能查看其他管理员的数据
  > 例：如下图所示，A给b1和c1分配任务，假设B拥有部门1和部门2的数据权限，则B只能查看b1和c1的该任务，不能对该任务进行删改的操作。<br>![avatar](../Authority/img/rule01.png)

* 用户上传的内容可以由超级管理员设置可见性
  > 1、默认情况下，管理员上传的内容只有该管理员直属上级部门，其所在部门及其所有子部门的人能看到。
  > 2、如果管理员同时属于多个部门，那么该管理员上传的内容，这几个部门的直属上级部门、这几个部门本身及其所有子部门都能看到。
  > 3、可以设置可见性的模块有：课程、会议、直播间、题目、试卷、考试、文档、文章、问卷、讲师、培训班、商品、擂台赛、投票、销售比拼、杏林说。

* 超级管理员可以将内容的可见性范围设置为多个部门
  > 例如：A部门管理员上传的课程，超级管理员可以将该课程设置为B、C、D部门都可见。

* 学习任务模块的可见性是只有发布者和发布者的上级能看到

* 各种分类列表和公告模块的可见性为所有人可见

* 所属关系的内容的可见性跟随主内容变动
  > 例如：A课程有a、b、c三条评论，那么a、b、c三条评论的可见性跟随A课程的可见性变动。

* 内容的作者（所属）不能被改变
  > 例如：A管理员上传课程a，超级管理员将课程a的可见性设置为全体人员都能看到，那么课程a的作者（所属）还是管理员A。

* 内容的可见性有两个部分不能被改变
  > 默认情况下，内容可见性包括三个部分：作者（所属）所在的部门、其直属上级部门、其所有子部门。这三个部分只有其所有子部门的可见性能被修改；作者（所属）所在的部门、其直属上级部门永远能看到该内容，并且不能被修改。

* 一个管理员能看的内容包含下属上传和直属上级开放的内容
  > 例如：如下图的部门结构（每个部门一个管理员）。E能看到的内容包括J和K上传的内容（查内容表）+A和B上传的内容并且该内容设置为对E可见（查内容可见性表）。<br>![avatar](../Authority/img/rule02.png)

## 2.产品架构
### 2.1 权限系统模型图
![avatar](../Authority/img/Model.png)

### 2.2 权限表
<table>
  <tr>
    <th>模块名称</th>
    <th>功能权限</th>
    <th>子功能权限</th>
  </tr>
  <tr>
    <td rowspan="3">课程管理</td>
    <td>课程管理</td>
    <td>查看课程、发布课程、编辑课程、上下架课程、删除课程</td>
  </tr>
  <tr>
    <td>课程分类管理</td>
    <td>查看分类、添加分类、编辑分类、删除分类</td>
  </tr>
  <tr>
    <td>课程评论管理</td>
    <td>查看课程评论、切换课程评论状态、删除课程评论</td>
  </tr>
  <tr>
    <td rowspan="3">会议管理</td>
    <td>会议管理</td>
    <td>查看会议、上传会议、编辑会议、上下架会议、删除会议</td>
  </tr>
  <tr>
    <td>会议分类管理</td>
    <td>查看分类、添加分类、编辑分类、删除分类</td>
  </tr>
  <tr>
    <td>会议评论管理</td>
    <td>查看会议评论、切换会议评论状态、删除会议评论</td>
  </tr>
  <tr>
    <td rowspan="4">学习地图管理</td>
    <td>能力项管理</td>
    <td>查看能力项、新建能力项、编辑能力项、删除能力项、导出能力项</td>
  </tr>
  <tr>
    <td>课程能力项匹配</td>
    <td>查看课程能力项匹配、设置能力项目</td>
  </tr>
  <tr>
    <td>学习路径管理</td>
    <td>查看学习路径、新建学习路径、编辑学习路径、删除学习路径</td>
  </tr>
  <tr>
    <td>学习地图管理</td>
    <td>查看学习地图、学习人员设置、查看学习记录、导出学习记录、导出详细学习记录</td>
  </tr>
  <tr>
    <td rowspan="4">成长带教管理</td>
    <td>任务库分类管理</td>
    <td>查看任务库分类、添加带教分类、编辑带教分类、删除带教分类</td>
  </tr>
  <tr>
    <td>带教任务库管理</td>
    <td>查看带教任务库、添加带教任务、编辑带教任务、删除带教任务</td>
  </tr>
  <tr>
    <td>带教计划设置</td>
    <td>查看带教计划、添加带教计划、复制计划任务、编辑带教计划、删除带教计划</td>
  </tr>
  <tr>
    <td>带教计划分配</td>
    <td>查看带教计划分配、添加带教计划分配、批量导入学员带教计划、导出学员带教计划、修改带教状态、查看带教计划进度、编辑带教计划分配、删除带教计划分配</td>
  </tr>
  <tr>
    <td rowspan="2">大赛中心管理</td>
    <td>比赛管理</td>
    <td>查看比赛管理、新建擂台、上下架擂台、编辑擂台、预览擂台、查看结果、删除擂台</td>
  </tr>
  <tr>
    <td>投票活动管理</td>
    <td>查看投票活动管理、新建投票活动、上下架投票活动、编辑投票活动、参与投票管理、删除投票活动</td>
  </tr>
  <tr>
    <td rowspan="5">明星讲师管理</td>
    <td>讲师管理</td>
    <td>查看讲师管理、新建讲师、查看讲师档案、编辑讲师、删除讲师</td>
  </tr>
  <tr>
    <td>讲师级别管理</td>
    <td>查看讲师级别管理、新增讲师级别、编辑讲师级别、删除讲师级别</td>
  </tr>
  <tr>
    <td>讲师专业领域管理</td>
    <td>查看讲师专业领域管理、新增讲师专业领域、编辑讲师专业领域、删除讲师专业领域</td>
  </tr>
  <tr>
    <td>讲师评论管理</td>
    <td>查看讲师评论、切换讲师评论状态、删除讲师评论</td>
  </tr>
  <tr>
    <td>讲师数据统计</td>
    <td>查看讲师数据统计、导出Excel</td>
  </tr>
  <tr>
    <td>能力测评管理</td>
    <td>能力测评管理</td>
    <td>查看能力测评管理、新建测评、上下架测评、分享测评、编辑测评、预览测评、查看测评结果、导出测评结果、删除答卷、删除测评</td>
  </tr>
  <tr>
    <td rowspan="4">知识共享管理</td>
    <td>文档管理</td>
    <td>查看文档管理、新建文档、编辑文档、删除文档</td>
  </tr>
  <tr>
    <td>文档分类管理</td>
    <td>查看文档分类管理、添加文档分类、编辑文档分类、删除文档分类</td>
  </tr>
  <tr>
    <td>文章管理</td>
    <td>查看文章管理、新建文章、编辑文章、删除文章</td>
  </tr>
  <tr>
    <td>文章分类管理</td>
    <td>查看文章分类管理、添加文章分类、编辑文章分类、删除文章分类</td>
  </tr>
  <tr>
    <td rowspan="2">动态管理</td>
    <td>公告管理</td>
    <td>查看公告管理、添加公告、编辑公告、删除公告</td>
  </tr>
  <tr>
    <td>公告分类管理</td>
    <td>查看公告分类管理、添加公告分类、编辑公告分类、删除公告分类</td>
  </tr>
  <tr>
    <td rowspan="3">积分商城管理</td>
    <td>商品管理</td>
    <td>查看商品管理、添加商品、上下架商品、编辑商品、删除商品</td>
  </tr>
  <tr>
    <td>商品分类管理</td>
    <td>查看商品分类管理、添加商品分类、编辑商品分类、删除商品分类</td>
  </tr>
  <tr>
    <td>订单管理</td>
    <td>查看订单管理、删除订单、标记订单状态</td>
  </tr>
  <tr>
    <td rowspan="2">互动问答管理</td>
    <td>问答管理</td>
    <td>查看问答管理、删除问答</td>
  </tr>
  <tr>
    <td>问答评论管理</td>
    <td>查看问答评论、切换问答评论状态、删除问答评论</td>
  </tr>
  <tr>
    <td rowspan="2">互动直播管理</td>
    <td>直播管理</td>
    <td>查看直播管理、添加直播间、上下架直播间、编辑直播间、查看直播间结果、删除直播间</td>
  </tr>
  <tr>
    <td>直播分类管理</td>
    <td>查看直播分类管理、添加直播分类、编辑直播分类、删除直播分类</td>
  </tr>
  <tr>
    <td rowspan="2">学习任务管理</td>
    <td>学习任务管理</td>
    <td>查看学习任务管理、发布学习任务、查看任务的学员列表、删除任务中的学员、编辑学习任务、删除学习任务</td>
  </tr>
  <tr>
    <td>任务进度查询</td>
    <td>任务进度查询</td>
  </tr>
  <tr>
    <td>培训班管理</td>
    <td>培训班管理</td>
    <td>查看培训班管理、添加培训班、查看培训班学员、删除培训班学员、编辑培训班、删除培训班</td>
  </tr>
  <tr>
    <td>问卷管理</td>
    <td>我的问卷管理</td>
    <td>查看问卷管理、新建问卷、上下架问卷、分享问卷、编辑问卷、预览问卷、查看问卷结果、导出问卷结果、删除问卷</td>
  </tr>
  <tr>
    <td rowspan="5">企业考试管理</td>
    <td>企业考试管理</td>
    <td>查看企业考试管理、新建考试、上下架考试、编辑考试、预览试卷、查看考试结果、导出考试结果、删除考试</td>
  </tr>
  <tr>
    <td>试卷管理</td>
    <td>查看试卷管理、新建试卷、编辑试卷、预览试卷、删除试卷</td>
  </tr>
  <tr>
    <td>试卷标签管理</td>
    <td>查看试卷标签管理、新建试卷标签、编辑试卷标签、删除试卷标签</td>
  </tr>
  <tr>
    <td>试题管理</td>
    <td>查看试题管理、添加试题、批量导入题目、编辑题目、删除题目</td>
  </tr>
  <tr>
    <td>试题标签管理</td>
    <td>查看试题标签管理、新建题目标签、编辑题目标签、删除题目标签</td>
  </tr>
</table>

## 3.页面说明
|页面编号|页面名称|页面主要功能介绍|
|:--:|:--:|:--:|
|P01|角色管理页面|展示角色列表，提供对角色的增删改查操作|
|P02|添加角色页面|添加新的角色到角色管理列表里面，并给角色设置功能权限|
|P03|编辑角色页面|对角色管理列表中已有角色的信息和功能权限进行修改|
|P04|关联人员页面|可以给每个角色关联人员|
|P05|数据权限管理页面|展示赋予了角色的人员列表|
|P06|设置数据权限页面|对赋予了角色的人员列表进行数据权限的设置|
|P07|人员管理页面|展示人员列表，只能进行查看操作|
|P08|部门管理页面|展示部门列表，只能进行查看操作|
|P09|可见性设置示例页面|管理员上传的内容可以由超级管理员修改可见性|
|P10|设置可见范围页面|设置可见范围|

#### 3.1.1 角色管理页面（P01）
<table>
  <tr>
      <img src="../img/p3_1_1.png"/>
  </tr>
  <tr>
    <th>编号</th>
    <th>名称</th>
    <th>功能、交互说明</th>
  </tr>
  <tr>
    <td>1</td>
    <td>页面路径</td>
    <td>显示当前页面的路径位置，该处不可点击</td>
  </tr>
  <tr>
    <td>2</td>
    <td>添加角色按钮</td>
    <td>点击弹出添加角色界面</td>
  </tr>
  <tr>
    <td>3</td>
    <td>角色列表</td>
    <td>展示角色相关信息的列表，包括角色名称、已关联人员和添加时间等</td>
  </tr>
  <tr>
    <td>4</td>
    <td>编辑按钮</td>
    <td>点击打开编辑角色界面</td>
  </tr>
  <tr>
    <td>5</td>
    <td>关联人员按钮</td>
    <td>点击打开关联人员页面</td>
  </tr>
  <tr>
    <td>6</td>
    <td>删除按钮</td>
    <td>点击之后弹窗，弹窗文案为：“是否删除所选角色”。选项为：【取消】和【确定】。点击取消，关闭弹窗；点击确定，删除所选角色，并关闭弹窗</td>
  </tr>
  <tr>
    <td>7</td>
    <td>分页</td>
    <td>将角色列表分页，用于显示角色总数、设置每页显示的角色数量和切换角色列表页数</td>
  </tr>
</table>

#### 3.1.2 添加角色页面（P02）
<table>
  <tr>
      <img src="../img/p3_1_2.png"/>
  </tr>
  <tr>
    <th>编号</th>
    <th>名称</th>
    <th>功能、交互说明</th>
  </tr>
  <tr>
    <td>1</td>
    <td>关闭按钮</td>
    <td>点击关闭该弹窗页面</td>
  </tr>
  <tr>
    <td>2</td>
    <td>角色名称输入框</td>
    <td>用于输入角色的名称。未填入内容时，输入框中显示提示文案：“请输入角色名称”。该项为必填项，在该项前面用红色星号标识，用户若未填写该项就点击确认添加按钮，则在该项右边出现红色提示文案：“未填写角色名称”</td>
  </tr>
  <tr>
    <td>3</td>
    <td>分配权限列表</td>
    <td>用于给角色分配权限。如果选择了上级角色，则该列表只显示上级角色的权限范围；如果没有选择上级角色，则该列表显示权限表中的全部权限</td>
  </tr>
  <tr>
    <td>4</td>
    <td>模块名称</td>
    <td>显示权限表中的模块名称部分</td>
  </tr>
  <tr>
    <td>5</td>
    <td>功能权限</td>
    <td>显示权限表中的功能权限部分。点击功能权限前面的勾选按钮，自动勾选该功能权限包含的所有子功能权限，再次点击则取消全部勾选</td>
  </tr>
  <tr>
    <td>6</td>
    <td>子功能权限</td>
    <td>显示权限表中的子功能权限部分。勾选增删改类型的权限时，自动勾选查看权限；取消勾选查看权限时，自动取消增删改类型的权限</td>
  </tr>
  <tr>
    <td>7</td>
    <td>确认添加按钮</td>
    <td>如果用户填好所有必填项，则提交该角色，关闭添加角色弹窗页面，并弹出提示弹窗，提示文案为：“添加成功”；如果用户没有填好所有必填项，则在相应地方显示提示文案</td>
  </tr>
</table>

#### 3.1.3 编辑角色页面（P03）
<table>
  <tr>
      <img src="../img/p3_1_3.png"/>
  </tr>
  <tr>
    <th>编号</th>
    <th>名称</th>
    <th>功能、交互说明</th>
  </tr>
  <tr>
    <td>1</td>
    <td>关闭按钮</td>
    <td>点击关闭该弹窗页面</td>
  </tr>
  <tr>
    <td>2</td>
    <td>角色名称输入框</td>
    <td>用于输入角色的名称。未填入内容时，输入框中显示提示文案：“请输入角色名称”。该项为必填项，在该项前面用红色星号标识，用户若未填写该项就点击确认添加按钮，则在该项右边出现红色提示文案：“未填写角色名称”</td>
  </tr>
  <tr>
    <td>3</td>
    <td>分配权限列表</td>
    <td>用于给角色分配权限。如果选择了上级角色，则该列表只显示上级角色的权限范围；如果没有选择上级角色，则该列表显示权限表中的全部权限</td>
  </tr>
  <tr>
    <td>4</td>
    <td>模块名称</td>
    <td>显示权限表中的模块名称部分</td>
  </tr>
  <tr>
    <td>5</td>
    <td>功能权限</td>
    <td>显示权限表中的功能权限部分。点击功能权限前面的勾选按钮，自动勾选该功能权限包含的所有子功能权限，再次点击则取消全部勾选</td>
  </tr>
  <tr>
    <td>6</td>
    <td>子功能权限</td>
    <td>显示权限表中的子功能权限部分。勾选增删改类型的权限时，自动勾选查看权限；取消勾选查看权限时，自动取消增删改类型的权限</td>
  </tr>
  <tr>
    <td>7</td>
    <td>确认修改按钮</td>
    <td>如果用户填好所有必填项，则提交该角色，关闭添加角色弹窗页面，并弹出提示弹窗，提示文案为：“修改成功”；如果用户没有填好所有必填项，则在相应地方显示提示文案</td>
  </tr>
</table>

#### 3.1.4 关联人员页面（P04）
<table>
  <tr>
      <img src="../img/p3_1_4.png"/>
  </tr>
  <tr>
    <th>编号</th>
    <th>名称</th>
    <th>功能、交互说明</th>
  </tr>
  <tr>
    <td>1</td>
    <td>关闭按钮</td>
    <td>点击关闭该弹窗页面</td>
  </tr>
  <tr>
    <td>2</td>
    <td>搜索框</td>
    <td>用于搜索部门，在框中输入关键字，自动搜索部门</td>
  </tr>
  <tr>
    <td>3</td>
    <td>部门结构</td>
    <td>用树形结构展示整个企业的部门结构</td>
  </tr>
  <tr>
    <td>4</td>
    <td>折叠按钮</td>
    <td>默认状态下为展开，点击可以折叠该项包含的所有子部门，再次点击可以展开该项包含的所有子部门</td>
  </tr>
  <tr>
    <td>5</td>
    <td>选中状态</td>
    <td>点击树形列表中的单个项，该项变为选中状态，并且右边表格中显示该项包含的下一级部门列表</td>
  </tr>
  <tr>
    <td>6</td>
    <td>关键字输入框</td>
    <td>在输入框中输入关键字（姓名/岗位/手机号/工号），点击搜索按钮即可搜索相应的人员，并在下方的列表中展示，未输入时框中显示提示文案：“请输入姓名/岗位/手机号/工号查询”</td>
  </tr>
  <tr>
    <td>7</td>
    <td>关联状态选择器</td>
    <td>点击之后出现下拉菜单，该菜单只有两个选项：【已关联】、【未关联】，选择一个选项，然后点击搜索按钮即可搜索相应的人员，并在下方的列表中展示</td>
  </tr>
  <tr>
    <td>8</td>
    <td>搜索按钮</td>
    <td>点击之后根据前面输入的关键字或者选择的关联状态查找相应的人员，并在下方的列表中展示。可以只根据一个条件搜索，也可以两个条件一起搜索</td>
  </tr>
  <tr>
    <td>9</td>
    <td>人员列表</td>
    <td>展示人员相关信息的列表，包括姓名、性别、手机号、工号、所在部门和所在岗位等</td>
  </tr>
  <tr>
    <td>10</td>
    <td>勾选器</td>
    <td>勾选时代表选择该人员关联该角色，勾选页头的勾选器可以快速全勾选该页所有人</td>
  </tr>
  <tr>
    <td>11</td>
    <td>分页</td>
    <td>将人员列表分页，用于显示人员总数、设置每页显示的人员数量和切换人员列表页数</td>
  </tr>
  <tr>
    <td>12</td>
    <td>确认关联按钮</td>
    <td>点击之后将已勾选的人员关联到该角色，关闭关联人员弹窗页面，并弹出提示弹窗，提示文案为：“关联成功”</td>
  </tr>
</table>

#### 3.1.5 数据权限管理页面（P05）
<table>
  <tr>
      <img src="../img/p3_1_5.png"/>
  </tr>
  <tr>
    <th>编号</th>
    <th>名称</th>
    <th>功能、交互说明</th>
  </tr>
  <tr>
    <td>1</td>
    <td>页面路径</td>
    <td>显示当前页面的路径位置，该处不可点击</td>
  </tr>
  <tr>
    <td>2</td>
    <td>姓名输入框</td>
    <td>在输入框中输入姓名，点击搜索按钮即可搜索相应的人员，并在下方的列表中展示</td>
  </tr>
  <tr>
    <td>3</td>
    <td>角色名称输入框</td>
    <td>在输入框中输入角色名称，点击搜索按钮即可搜索拥有该角色的相应的人员，并在下方的列表中展示</td>
  </tr>
  <tr>
    <td>4</td>
    <td>搜索按钮</td>
    <td>点击之后根据前面输入的姓名或者角色名称查找相应的人员，并在下方的列表中展示。可以只根据一个条件搜索，也可以两个条件一起搜索</td>
  </tr>
  <tr>
    <td>5</td>
    <td>管理员列表</td>
    <td>只有分配了角色的人员才能在该列表中显示，该列表内容包含姓名和已关联角色名称</td>
  </tr>
  <tr>
    <td>6</td>
    <td>设置数据权限按钮</td>
    <td>点击打开设置数据权限页面</td>
  </tr>
  <tr>
    <td>7</td>
    <td>分页</td>
    <td>将管理员列表分页，用于显示管理员总数、设置每页显示的管理员数量和切换管理员列表页数</td>
  </tr>
</table>

#### 3.1.6 设置数据权限页面（P06）
<table>
  <tr>
      <img src="../img/p3_1_6.png"/>
  </tr>
  <tr>
    <th>编号</th>
    <th>名称</th>
    <th>功能、交互说明</th>
  </tr>
  <tr>
    <td>1</td>
    <td>关闭按钮</td>
    <td>点击关闭该弹窗页面，并且不保存任何操作内容</td>
  </tr>
  <tr>
    <td>2</td>
    <td>搜索框</td>
    <td>用于搜索部门，在框中输入关键字，自动搜索部门</td>
  </tr>
  <tr>
    <td>3</td>
    <td>部门结构</td>
    <td>用树形结构展示整个企业的部门结构</td>
  </tr>
  <tr>
    <td>4</td>
    <td>折叠按钮</td>
    <td>默认状态下为展开，点击可以折叠该项包含的所有子部门，再次点击可以展开该项包含的所有子部门</td>
  </tr>
  <tr>
    <td>5</td>
    <td>勾选器</td>
    <td>点击则勾选该部门，再次点击取消勾选。勾选则代表将该部门的数据权限分配给该管理员用户。勾选状态分为两种，一种为用户主动点击勾选；另一种为系统自动勾选，系统自动勾选的样式为灰色勾选，不允许用户点击取消勾选</td>
  </tr>
  <tr>
    <td>6</td>
    <td>部门名字输入框</td>
    <td>在输入框中输入部门名字，点击搜索按钮即可搜索已勾选的相应的部门，并在下方的列表中展示</td>
  </tr>
  <tr>
    <td>7</td>
    <td>搜索按钮</td>
    <td>点击之后可以根据部门名字输入框中输入的内容进行搜索</td>
  </tr>
  <tr>
    <td>8</td>
    <td>数据权限操作设置列表</td>
    <td>用于设置已选择的数据范围的数据权限操作的列表</td>
  </tr>
  <tr>
    <td>9</td>
    <td>勾选器</td>
    <td>勾选时代表选择该部门，勾选页头的勾选器可以快速全勾选该页所有部门</td>
  </tr>
  <tr>
    <td>10</td>
    <td>已选择数据权限范围</td>
    <td>该列内容为左边树形结构里面已勾选的部门，格式为：前面用灰色从根级别一直显示到上一级别，最后面该部门的名字用黑色字体显示</td>
  </tr>
  <tr>
    <td>11</td>
    <td>数据权限范围扩展</td>
    <td>每个已选择的部门均可扩展范围，扩展范围有两个选项：【仅本部门】、【本部门及其所有子部门】，该选项为单选。如果选择仅本部门，数据权限的范围就只有本部门；如果选择本部门及其所有子部门，则数据权限的范围为本部门及其所有子部门，并且在左边的树形结构中自动勾选该部门的所有子部门（自动勾选的部门不允许用户点击取消勾选，样式为灰色勾选），但是所有子部门并不在该列表中显示出来</td>
  </tr>
  <tr>
    <td>12</td>
    <td>删除按钮</td>
    <td>点击之后弹窗，弹窗文案为：“是否删除所选数据范围”。选项为：【取消】和【确定】。点击取消，关闭弹窗；点击确定，删除所有勾选的数据范围，并关闭弹窗</td>
  </tr>
  <tr>
    <td>13</td>
    <td>分页</td>
    <td>将已选数据权限范围列表分页，用于显示已选数据权限范围总数、设置每页显示的已选数据权限范围数量和切换已选数据权限范围列表页数</td>
  </tr>
  <tr>
    <td>14</td>
    <td>确认按钮</td>
    <td>点击之后保存设置好的数据权限，关闭设置数据权限弹窗页面，并弹出提示弹窗，提示文案为：“设置成功”</td>
  </tr>
</table>

#### 3.1.7 人员管理页面（P07）
<table>
  <tr>
      <img src="../img/p3_1_7.png"/>
  </tr>
  <tr>
    <th>编号</th>
    <th>名称</th>
    <th>功能、交互说明</th>
  </tr>
  <tr>
    <td>1</td>
    <td>页面路径</td>
    <td>显示当前页面的路径位置，该处不可点击</td>
  </tr>
  <tr>
    <td>2</td>
    <td>姓名输入框</td>
    <td>在输入框中输入姓名，点击搜索按钮即可搜索相应的人员，并在下方的列表中展示</td>
  </tr>
  <tr>
    <td>3</td>
    <td>部门选择器</td>
    <td>点击之后出现下拉菜单，点击菜单中的部门选项，然后点击搜索按钮即可搜索相应的部门人员，并在下方的列表中展示</td>
  </tr>
  <tr>
    <td>4</td>
    <td>搜索按钮</td>
    <td>点击之后根据前面输入的姓名或者选好的部门查询相关人员，并在下方的列表中展示。可以只根据一个条件搜索，也可以两个条件一起搜索</td>
  </tr>
  <tr>
    <td>5</td>
    <td>人员列表</td>
    <td>展示人员相关信息的列表，包括姓名、性别、手机号、工号、所在部门、所在岗位和已关联角色等</td>
  </tr>
  <tr>
    <td>6</td>
    <td>分页</td>
    <td>将人员列表分页，用于显示人员总数、设置每页显示的人员数量和切换人员列表页数</td>
  </tr>
</table>

#### 3.1.8 部门管理页面（P08）
<table>
  <tr>
      <img src="../img/p3_1_8.png"/>
  </tr>
  <tr>
    <th>编号</th>
    <th>名称</th>
    <th>功能、交互说明</th>
  </tr>
  <tr>
    <td>1</td>
    <td>页面路径</td>
    <td>显示当前页面的路径位置，该处不可点击</td>
  </tr>
  <tr>
    <td>2</td>
    <td>搜索框</td>
    <td>用于搜索部门，在框中输入关键字，自动搜索部门</td>
  </tr>
  <tr>
    <td>3</td>
    <td>部门结构</td>
    <td>用树形结构展示整个企业的部门结构</td>
  </tr>
  <tr>
    <td>4</td>
    <td>折叠按钮</td>
    <td>默认状态下为展开，点击可以折叠该项包含的所有子部门，再次点击可以展开该项包含的所有子部门</td>
  </tr>
  <tr>
    <td>5</td>
    <td>选中状态</td>
    <td>点击树形列表中的单个项，该项变为选中状态，并且右边表格中显示该项包含的下一级部门列表</td>
  </tr>
  <tr>
    <td>6</td>
    <td>导航</td>
    <td>显示当前列表是哪个公司的哪个部门。根据该部门在左边树形列表结构来显示每个部分的内容，点击每个部分可以显示相应的部分的下一级部门列表</td>
  </tr>
  <tr>
    <td>7</td>
    <td>部门名称输入框</td>
    <td>在输入框中输入部门名称，点击搜索按钮即可搜索相应的部门，并在下方的列表中展示</td>
  </tr>
  <tr>
    <td>8</td>
    <td>搜索按钮</td>
    <td>点击之后根据前面输入的部门名称查询相关部门，并在下方的列表中展示</td>
  </tr>
  <tr>
    <td>9</td>
    <td>部门列表</td>
    <td>显示部门相关信息的列表，包含部门名称、子部门数和部门人数等</td>
  </tr>
  <tr>
    <td>10</td>
    <td>子部门数排序</td>
    <td>该按钮分为上下两个箭头，初始都为灰色。点击上面的箭头，将列表按照子部门数升序排列；点击下面的箭头，将列表按照子部门数降序排列；点击旁边的空白，恢复列表初始排序，并将按钮重置为初始状态</td>
  </tr>
  <tr>
    <td>11</td>
    <td>下级部门按钮</td>
    <td>点击之后显示该部门的下一级部门列表，并替换掉现在的部门列表。导航部分也做相应的位置更改</td>
  </tr>
</table>

#### 3.1.9 可见性设置示例页面（P09）
<table>
  <tr>
      <img src="../img/p3_1_9.png"/>
  </tr>
  <tr>
    <th>编号</th>
    <th>名称</th>
    <th>功能、交互说明</th>
  </tr>
  <tr>
    <td>1</td>
    <td>可见范围列</td>
    <td>显示该条内容当前的可见范围，格式为：“部门1、部门2”超出部分用省略号显示</td>
  </tr>
  <tr>
    <td>2</td>
    <td>tooltip信息</td>
    <td>鼠标移动到【1】上，如果有超出的部分，则使用tooltip显示完整的可见范围信息；如果没有超出部分，则不显示</td>
  </tr>
  <tr>
    <td>3</td>
    <td>设置可见范围按钮</td>
    <td>点击打开设置可见范围页面。需要添加该按钮的模块有：课程、会议、直播间、题目、试卷、考试、文档、文章、问卷、讲师、培训班、商品、擂台赛、投票</td>
  </tr>
</table>

#### 3.1.10 设置可见范围页面（P10）
<table>
  <tr>
      <img src="../img/p3_1_10.png"/>
  </tr>
  <tr>
    <th>编号</th>
    <th>名称</th>
    <th>功能、交互说明</th>
  </tr>
  <tr>
    <td>1</td>
    <td>关闭按钮</td>
    <td>点击关闭该弹窗页面，并且不保存任何操作内容</td>
  </tr>
  <tr>
    <td>2</td>
    <td>搜索框</td>
    <td>用于搜索部门，在框中输入关键字，自动搜索部门</td>
  </tr>
  <tr>
    <td>3</td>
    <td>部门结构</td>
    <td>用树形结构展示整个企业的部门结构</td>
  </tr>
  <tr>
    <td>4</td>
    <td>折叠按钮</td>
    <td>默认状态下为展开，点击可以折叠该项包含的所有子部门，再次点击可以展开该项包含的所有子部门</td>
  </tr>
  <tr>
    <td>5</td>
    <td>勾选器</td>
    <td>点击则勾选该部门，再次点击取消勾选。勾选则代表此内容对该部门可见。勾选状态分为两种，一种为用户主动点击勾选；另一种为系统自动勾选，系统自动勾选的样式为灰色勾选，不允许用户点击取消勾选</td>
  </tr>
  <tr>
    <td>6</td>
    <td>部门名字输入框</td>
    <td>在输入框中输入部门名字，点击搜索按钮即可搜索已勾选的相应的部门，并在下方的列表中展示</td>
  </tr>
  <tr>
    <td>7</td>
    <td>搜索按钮</td>
    <td>点击之后可以根据部门名字输入框中输入的内容进行搜索</td>
  </tr>
  <tr>
    <td>8</td>
    <td>可见范围操作设置列表</td>
    <td>用于设置内容对哪些部门可见的操作列表</td>
  </tr>
  <tr>
    <td>9</td>
    <td>勾选器</td>
    <td>勾选时代表选择该部门，勾选页头的勾选器可以快速全勾选该页所有部门</td>
  </tr>
  <tr>
    <td>10</td>
    <td>已选择数据权限范围</td>
    <td>该列内容为左边树形结构里面已勾选的部门，格式为：前面用灰色从根级别一直显示到上一级别，最后面该部门的名字用黑色字体显示</td>
  </tr>
  <tr>
    <td>11</td>
    <td>可见范围扩展</td>
    <td>每个已选择的部门均可扩展范围，扩展范围有两个选项：【仅本部门】、【本部门及其所有子部门】，该选项为单选。如果选择仅本部门，可见范围就只有本部门；如果选择本部门及其所有子部门，则可见范围为本部门及其所有子部门，并且在左边的树形结构中自动勾选该部门的所有子部门（自动勾选的部门不允许用户点击取消勾选，样式为灰色勾选），但是所有子部门并不在该列表中显示出来</td>
  </tr>
  <tr>
    <td>12</td>
    <td>删除按钮</td>
    <td>点击之后弹窗，弹窗文案为：“是否删除所选可见范围”。选项为：【取消】和【确定】。点击取消，关闭弹窗；点击确定，删除所有勾选的可见范围，并关闭弹窗</td>
  </tr>
  <tr>
    <td>13</td>
    <td>分页</td>
    <td>将已选可见范围列表分页，用于显示已选可见范围总数、设置每页显示的已选可见范围数量和切换已选可见范围列表页数</td>
  </tr>
  <tr>
    <td>14</td>
    <td>确认按钮</td>
    <td>点击之后保存设置好的可见范围，关闭设置可见范围弹窗页面，并弹出提示弹窗，提示文案为：“设置成功”</td>
  </tr>
</table>
