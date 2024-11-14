[合集 \- 玩转Streamlit(8\)](https://github.com)[1\.什么是Streamlit10\-11](https://github.com/wang_yb/p/18458062)[2\.『玩转Streamlit』\-\-环境配置10\-17](https://github.com/wang_yb/p/18471660)[3\.『玩转Streamlit』\-\-架构和运行机制10\-22](https://github.com/wang_yb/p/18492213)[4\.『玩转Streamlit』\-\-多页应用10\-25](https://github.com/wang_yb/p/18502232):[豆荚加速器](https://yirou.org)[5\.『玩转Streamlit』\-\-页面布局10\-31](https://github.com/wang_yb/p/18516928)[6\.『玩转Streamlit』\-\-登录认证机制11\-05](https://github.com/wang_yb/p/18527320)[7\.『玩转Streamlit』\-\-文本与标题组件11\-07](https://github.com/wang_yb/p/18531821)8\.『玩转Streamlit』\-\-数据展示组件11\-13收起
数据展示组件在`Streamlit`各类组件中占据了至关重要的地位，


它的核心功能是以直观、易于理解的方式展示数据。


本次介绍的数据展示组件`st.dataframe`和`st.table`，能够将复杂的数据集以表格、图表等形式清晰地呈现出来，使得用户能够快速把握数据的整体情况和细节特征。


# 1\. st.dataframe


`st.dataframe`以易读且美观的方式展示`pandas`的`DataFrame`。


无论是处理小型数据集还是庞大的数据表，`st.dataframe`都能轻而易举展示数据。


`st.dataframe`适用于需要在Web应用中展示复杂数据集的场景。


首先，它能够自动适应屏幕宽度，并支持水平或垂直滚动，确保用户能方便地浏览整个数据集。


此外，`st.dataframe`还支持对数据进行排序、筛选和搜索等操作，增强了数据的可读性和交互性。


# 2\. st.table


`st.table`也是用于在Web应用中显示表格数据，


它可以显示交互式表格，并提供多种自定义设置来满足各类需求。


与`st.dataframe`相比，`st.table`更适用于当**数据集不是特别庞大**且需要保持清晰可读性的场景。


它允许用户通过简单的配置来调整表格的显示方式，如列宽、行高等。


# 3\. 两者区别


这两个组件都用于展示数据，都支持多种类型的数据对象作为输入，比如`pandas.DataFrame`，`numpy.ndarray`、`Iterable`、`dict`等等。


但是在**交互性**，**显示方式**和**功能丰富度**上面是有区别的，


下面通过一个示例来演示两者在使用上的区别，


先使用 `st.dataframe` 显示一个包含用户信息的静态`DataFrame`，如姓名、年龄和邮箱。


`DataFrame`将显示为可滚动、可排序和可搜索的表格。还可以将数据保存为`CSV`文件。


同样使用 st.table 显示相同的用户信息数据集，但表格样式会更加简洁，功能相对较少（例如，不支持搜索）。



```
import streamlit as st
import pandas as pd

# 创建静态数据集
data = {
    "姓名": ["张三", "李四", "王五"],
    "年龄": [25, 30, 35],
    "邮箱": ["zhangsan@example.com", "lisi@example.com", "wangwu@example.com"],
}
df = pd.DataFrame(data)

st.header("st.dataframe")
# 使用st.dataframe显示
st.dataframe(df)

st.header("st.table")
# 使用st.table显示
st.table(df)

```

![](https://img2024.cnblogs.com/blog/83005/202411/83005-20241113130840934-1996714055.gif)


除了功能比较丰富以外，`st.dataframe`对于展示千上万行的大型数据集时，可以调整其高度和宽度，可以搜索过滤和排序，因此更方便遇查看数据。


而`st.table`由于功能相对简单，会将所有数据直接展示出来，浏览和分析大量数据不那么方便。


比如，下面模拟了一个一万条数据的场景。


`st.dataframe`展示时，可以固定一块位置；而`st.table`将所有数据平铺下去展示，加装时间也明显长很多。



```
# 创建大数据集
np.random.seed(0)
data = {
    "ID": np.arange(1, 10001),
    "值1": np.random.rand(10000),
    "值2": np.random.rand(10000),
    # ... 可以添加更多列
}
df = pd.DataFrame(data)

st.header("st.dataframe", width=400, height=600)
# 使用st.dataframe显示大数据集
st.dataframe(df)

st.header("st.table")
# 使用st.table显示大数据集（可能性能不佳）
# 对于大数据集，st.table可能不是最佳选择
st.table(df)

```

![](https://img2024.cnblogs.com/blog/83005/202411/83005-20241113130841079-957656296.gif)


# 4\. 总结


总得来看，`st.dataframe` 更适合需要高级功能和动态交互的场景，


而 `st.table` 则更适合简单、快速的表格展示。


