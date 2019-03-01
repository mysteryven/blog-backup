---
title: Echarts填坑
date: 2018-03-16 17:44:55
tags: echarts
categories: 编程

---


这三天，被一个流程图折磨的要命，刚开始用的是 HighLight，感觉文档很是晦涩难懂，后来换了【echarts】，用起来舒服多了。 
但是也是遇到了几个地方，下面整理一下遇到的问题。

<!-- more -->

## 1. 异步更新数据
异步更新数据就是当在ajax的函数里面取到数据之后，在` myChart.setOption({}）`里面添加时关于系列的数据就好了
系列中，可以添加[data.x, data.y]的格式。

## 2. 根据需求给点设置不同的颜色
series里面写的就是每个点，在series设置itemstyle属性即可，具体根据下面代码设置：

```
series: [{
	name: '工序',
	type: 'bar',
	data: viewModel.processAndTime(),
	itemStyle: {
	    normal: {
            color: function(params) {
            	var colorList = viewModel.colorList();
            	return colorList[params.dataIndex];
            }
        }
	}
```

## 3. 散点图的形状
设置symbol属性
取值有triangle， diamond， circle等

## 4. 在一副表中显示多个图
在series里面添加对象即可

## 5. 设置柱形图的宽度 间隔 圆角

- barWidth
- interval
- 圆角

```
itemStyle: {
	normal: {
        barBorderRadius: 10
    },
	emphasis: {	
        barBorderRadius: 10
    }
},
```


## 6. 显示两个坐标轴
比如，显示两个x轴，那就在xAxis下加两个对象，比如

```
xAxis: [
	{	
		data: data1
		type: 'time'
	}
	{
		type: 'category'
		data: data2
	}
]
                            
```

之后你还要在series的添加类似于`xAxisIndex: 1`的数据,如果不使用添加的坐标轴，他会不显示。


# 7 以时间为x轴的横道图(抄的别人的代码)
```
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        html, body {
            width: 100%;
            height: 100%;
            background: #020202;
            overflow: hidden;
        }

        #container {
            width: 100%;
            height: 100%;
        }
    </style>
</head>
<body>
<div id="container"></div>
</body>
<script src="https://cdn.bootcss.com/jquery/3.3.1/core.js"></script>
<script src="https://cdn.bootcss.com/echarts/4.0.4/echarts-en.common.js"></script>
<script>
    //计算两个日期相差天数
    function  DateDiff(sDate1,sDate2){    
    //sDate1和sDate2是2006-12-18格式
        var aDate,oDate1,oDate2,iDays;
        aDate = sDate1.split("-");
        oDate1 = new Date(aDate[1]+'-'+aDate[2]+'-'+aDate[0]) ;   
        aDate = sDate2.split("-");
        oDate2 = new Date(aDate[1]+'-'+aDate[2]+'-'+aDate[0]);
        iDays = parseInt(Math.abs(oDate1-oDate2)/1000/60/60/24)    ;//把相差的毫秒数转换为天数
        return iDays;
    }

    //获得两个日期间所有日期-fn1
    Date.prototype.format = function() {
        var s = '';
        var mouth = (this.getMonth()+1)>=10?(this.getMonth()+1):('0'+(this.getMonth() + 1));
        var day = this.getDate()>=10?this.getDate():('0'+this.getDate());
        s += this.getFullYear()+'-'; // 获取年份。
        s += mouth + "-"; // 获取月份。
        s += day;   //获取日。
        return (s); //返回日期。
    };
    //获得两个日期间所有日期-fn2
    function getAll(begin, end) {
        var return_=[];
        var ab = begin.split("-");
        var ae = end.split("-");
        var db = new Date();
        db.setUTCFullYear(ab[0], ab[1] - 1, ab[2]);
        var de = new Date();
        de.setUTCFullYear(ae[0], ae[1] - 1, ae[2]);
        var unixDb = db.getTime();
        var unixDe = de.getTime();
        for (var k = unixDb; k <= unixDe;) {
            return_.push((new Date(parseInt(k))).format());
            k = k + 24 * 60 * 60 * 1000;
        }
        return return_;
    }


    var dataa = [
        {
        "name":"项目a",
        "startTime":"2017-08-06",
        "latestTime":"2017-08-19"
        },
        {
        "name":"项目b",
        "startTime":"2017-08-14",
        "latestTime":"2017-08-17"
        }
    ];//假数据，实际应用可以用ajax从后台请求，获取数据
    var start_="2017-08-01",end_="2017-08-29";//用户自定义时间
    var data$ = DateDiff(start_,end_);//用户自定义的时间长度
    var data1 = DateDiff(start_,dataa[0].startTime);//项目a 起始位置
    var data1_1 = DateDiff(dataa[0].startTime,dataa[0].latestTime);//项目a 持续时间
    var data2 = DateDiff(start_,dataa[1].startTime);//项目b 起始位置
    var data2_1 = DateDiff(dataa[1].startTime,dataa[1].latestTime);//项目b 持续时间
    x_ = getAll(start_,end_);

    var myCharts =echarts.init(document.getElementById("container"));
    var option = {
        tooltip: {
            trigger: 'axis',
            axisPointer: {            
                type: 'shadow'      
            },
            formatter: function (params) {
                console.log(params);
                var tar = params[1];
                return tar.name + '<br/>' + tar.seriesName + ' :::: ' + tar.value;
            }
        },
        grid: {
            left: '3%',
            right: '4%',
            bottom: '3%',
            containLabel: true
        },
        xAxis: {
            type: 'value',
            max:data$,
             axisLabel: {
                 formatter: function (value, index) {
                    console.log(value);
                    return x_[value]
                 }
             }
        },
        yAxis: {
            type: 'category',
            splitLine: {show: false},
            data: ['项目a', '项目b']
        },
        series: [
            {
                name: '辅助',
                type: 'bar',
                stack: '总量',
                itemStyle: {
                    normal: {
                        barBorderColor: 'rgba(0,0,0,0)',
                        color: 'rgba(0,0,0,0)'
                    },
                    emphasis: {
                        barBorderColor: 'rgba(0,0,0,0)',
                        color: 'rgba(0,0,0,0)'
                    }
                },
                data: [data1,data2]
            },
            {
                //每个项目 持续时间长度
                name: '时长',
                type: 'bar',
                stack: '总量',
                label: {
                    normal: {
                        show: true,
                        position: 'inside'
                    }
                },
                data: [data1_1,data2_1]
            }
        ]
    };

    myCharts.setOption(option);

</script>
</html>
```