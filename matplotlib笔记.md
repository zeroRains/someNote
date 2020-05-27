# matplotlib简单应用

> 具体代码参考day01和day02中的内容

## 一、matplotlib——plot

1. axis 是轴的意思，x轴或者y轴
2. plot(x,y)**直线图**
3. figure中的`figsize=（20，8）`设置图片大小，宽20高8
4. `dpi` 每英寸上的像素点的个数
5. 对于画出的图片可使用`plt.savefig(路径)`进行保存。用.svg就可以变成矢量图
6. plt.xticks(a,b)
    * a表示原来的数值，b表示用来替换的字符串
    * 当想让字符串成为x轴的刻度时，可以使用一个变量记录所有的字符串，然后在进行一一对应
    * 例如：

    ```html
    _xtick_labels = ["10点{}分".format(i) for i in range(60)]
    _xtick_labels += ["11点{}分".format(i) for i in range(60)]
    ```

    * 然后用

    ```html
    plt.xticks(list(x)[::3],_xtick_labels[::3],rotation=45,fontproperties=my_font)
    ```

    * 将原来数值型x轴与字符串型进行等价切片从而实现用字符串代替数值
    * `rotation=45`是指字符串的**倾斜角度**
7. 如果字符串中含有中文应该事先设置然后用`fontproperties = font`属性设置  下面是font对应的设置方式  

    ```html
    from matplotlib import font_manager
    font=font_manager.FontProperties(fname=r"c:\\windows\\fonts\\simsun.ttc", size=16)
    ```

8. 添加描述信息：

    ```html
     plt.xlabel("时间",fontproperties=my_font)
    plt.ylabel("温度 单位(℃)",fontproperties=my_font)
    plt.title("10点到12点每分钟的气温变化情况",fontproperties=my_font)
    ```

     第一行的内容表示x轴的标签，第二行y轴的标签，第三行表示图表的名称

9. 给绘制出来的图形添加网格`plt.grid()`
    * `alpha`属性用来设置网格的透明度（取值0~1）

10. 画多条线
     * 使用两次`plt.plot(x,y)`传递不同的参数进去，然后会画出两条线
     * 使用`color`属性进行区分,`label`属性进行标记
     * `linestyle`属性表示的是线的风格 ：表示虚线，-. 表示点画线，--表示短线
     * 网格也能设置`linestyle`
     * `alpha`线条也可以设置这个透明度
     * `linewidth`表示线条的宽度
11. 图例：plt.legend()
     * 会显示出一个图例，然后我们的标记是中文需要设置`prop=font`属性进行调整
     * `loc`属性表示位置可以看源码找具体参数  0是最佳位置

## 二、matlab —— scatter —— 散点图

1. **绘制方法**：plt.scatter(x,y)
    * 只需传递x的数值，和y的数值，可以使元组列表集合

2. 属性和plot的差不多，基本都有了

## 三、matlab —— bar、barh —— 条形图

1. bar是竖直的条形图，barh是水平的条形图

2. plt.bar(x,y)
    * 同样只需传递x和y的数值,可以使用元组列表集合
    * x,y的值应该是数值，如果想改变坐标轴的标签为字符串需要用xticks
    * 可设置`width`属性表示条形的粗细
3. plt.barh(x,y)
    * 同样只需传递x和y的数值,可以使用元组列表集合
    * 可设置`height`属性表示条形的粗细   （**与bar区别开来**）

## 四、matlab —— hist —— 直方图

1. plt.hist(a,num_bins)
    * a是传入的数据集，num_bins是将其分成多少组
    * 如果组距不全是一样的num_bins可以传入一个数组
    * `normede`参数默认为False，使得y轴显示频数，改为True后显示频率

2. 数据分组
    * 100以内我们通常分成5~12组
    * 确认组距
    * 组距 = （最大值 - 最小值）/ 组数
    * 极差 / 组数的值要为整数，否则强制取整的话会产生偏差

3. 设置x轴的刻度
    * `plt.xticks(range(min(a) - min(a)+组距),组距)`

4. 绘制网格plt.grid()

## 五、饼图——pie

1. 直接看实例
    * `plt.pie([15,50,35],explode=(0,0,0.1),labels=labels,autopct='%1.1f%%',startangle = 90)`
    * `plt.axis('equal')`
    * 第一个列表表示每一部分数据所占的比例
    * explode:表示每块图形间的距离，第三个设置为0.1，有利于突出第三个数据
    * labels:对应数据的名称
    * autopct:对精度进行规范化
    * startangle：表示第一块饼图与x轴正方向的夹角角度
    * `plt.axis('equal')`必不可少，使X轴与Y轴的刻度保持一致

## 六、补充

1. 子图
    * 先使用`fig = plt.figure()`来开辟画布
    * 然后使用`ax1 = fig.add_subplot(2,2,1)`来选择分区，这里的2,2,1指的是在画布中分成了2x2的网格，我们选中他的第一个区域(左上角为第一区域，然后依次右移递增），这里的2,2,1参数也可以写成221
    * 因为分成了四块区域，所以ax2,ax3,ax4分别代表四块不同的区域
    * 我们直接ax1.绘图方式，就可以在第一区域绘图，其他同理
2. 给对应的曲线命名
    * `A，=plt.plot()`这样，你现在绘制的这条曲线就被命名为A
    * 当我们做图例的时候`plt.legend([A],["A"])`就能产生图例
    * 这个图例函数的两个参数都是填写列表或元组，分别对应的是绘制曲线的名称，以及对这条曲线的解释，记得一定要一一对应
    * 对于子图的图例将plt改成对应的命名区域就可

## 七、使用总结

1. 明确问题
2. 选择图形的呈现方式
3. 准备数据
4. 绘图和图形完善
5. 更多样式请参考 <a href="http://matplotlib.org/gallery">http://matplotlib.org/gallery</a>
