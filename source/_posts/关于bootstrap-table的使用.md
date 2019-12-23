---
title: 关于bootstrap-table的使用
typora-root-url: ..
date: 2019-10-17 16:58:57
tags: bootstrap
categories: bootstrap
password:
top:
---

> 1. 需要注意必需文件引入顺序
> 2. 注意jQuery版本会导致图标不显示的问题
> 3. 中文table要放在bootstrap-tablew.js文件下面

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<!-- <link rel="stylesheet" href="./css/bootstrap.css">
<link rel="stylesheet" href="./bootstrap-table-master/dist/bootstrap-table.min.css"> -->
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.2.1/css/bootstrap.min.css" integrity="sha384-GJzZqFGwb1QTTN6wy59ffF1BuGJpLSa9DkKMp0DgiMDm4iYMj70gZWKYbI706tWS" crossorigin="anonymous">
<link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.6.3/css/all.css" integrity="sha384-UHRtZLI+pbxtHCWp1t77Bi1L4ZtiqrqD80Kn4Z8NTSRyMA2Fd33n5dQ8lWUE00s/" crossorigin="anonymous">
<link rel="stylesheet" href="https://unpkg.com/bootstrap-table@1.15.3/dist/bootstrap-table.min.css">
<style>
#table1{
    width: 500px;
    /* height: 800px; */
    border: 1px solid #f40;
}
#table1 > thead th {
    padding: 0;
    margin: 0;
    background-color: #d9edf7;
}
#table1 tr:nth-child(even){
background:#f4f8fb;
}
</style>
<body>
	<div>
		<div class="page-table">
			<table id="table1"></table>
			<div class="fixed-table-pagination">
				<div class="pull-right pagination-detail">
					<span class="pagination-info">显示第 1 到第 <i></i> 条记录，总共<i></i> 条记录</span>
				</div>
			</div>
		</div>
	</div>
</body>
<!-- <script src="./js/jquery-1.12.4.js"></script>
<script src="./js/bootstrap.min.js"></script>
<script src="./bootstrap-table-master/dist/bootstrap-table.js"></script> -->
<!-- <script src="./bootstrap-table-master/dist/locale/bootstrap-table-zh-CN.js"></script> -->

<script src="https://code.jquery.com/jquery-3.3.1.min.js" integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8=" crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.6/umd/popper.min.js" integrity="sha384-wHAiFfRlMFy6i5SRaxvfOCifBUQy1xHdJ/yoi7FRNXMRBu5WHdZYu1hA6ZOblgut" crossorigin="anonymous"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.2.1/js/bootstrap.min.js" integrity="sha384-B0UglyR+jN6CkvvICOB2joaf5I4l3gm9GU6Hc1og6Ls7i6U/mkkaduKaBhlAXv9k" crossorigin="anonymous"></script>
<script src="https://unpkg.com/bootstrap-table@1.15.3/dist/bootstrap-table.min.js"></script>
<script src="./bootstrap-table-master/dist/locale/bootstrap-table-zh-CN.js"></script>

<script>

    //表格
    var data=[{
        "task":"水库日常巡查",
        "problemType":"电话举报",
        "arranger":"陈超",
        "patrols":"文湘",
        "beginTime":"2018-08-26",
        "endTime":"2018-08-27",
        "taskState":"已完成"
    },{
        "task":"水库日常巡查",
        "problemType":"电话举报",
        "arranger":"陈超",
        "patrols":"文湘",
        "beginTime":"2018-08-26",
        "endTime":"2018-08-27",
        "taskState":"已完成"
    },{
        "task":"水库日常巡查",
        "problemType":"电话举报",
        "arranger":"陈超",
        "patrols":"文湘",
        "beginTime":"2018-08-26",
        "endTime":"2018-08-27",
        "taskState":"已完成"
    },{
        "task":"水库日常巡查",
        "problemType":"电话举报",
        "arranger":"陈超",
        "patrols":"文湘",
        "beginTime":"2018-08-26",
        "endTime":"2018-08-27",
        "taskState":"未完成"
    },{
        "task":"水库日常巡查",
        "problemType":"电话举报",
        "arranger":"陈超",
        "patrols":"文湘",
        "beginTime":"2018-08-26",
        "endTime":"2018-08-27",
        "taskState":"已完成"
    },{
        "task":"水库日常巡查",
        "problemType":"电话举报",
        "arranger":"陈超",
        "patrols":"文湘",
        "beginTime":"2018-08-26",
        "endTime":"2018-08-27",
        "taskState":"未完成"
    },{
        "task":"水库日常巡查",
        "problemType":"电话举报",
        "arranger":"陈超",
        "patrols":"文湘",
        "beginTime":"2018-08-26",
        "endTime":"2018-08-27",
        "taskState":"已完成"
    },{
        "task":"水库日常巡查",
        "problemType":"电话举报",
        "arranger":"陈超",
        "patrols":"文湘",
        "beginTime":"2018-08-26",
        "endTime":"2018-08-27",
        "taskState":"已完成"
    },{
        "task":"水库日常巡查",
        "problemType":"电话举报",
        "arranger":"陈超",
        "patrols":"文湘",
        "beginTime":"2018-08-26",
        "endTime":"2018-08-27",
        "taskState":"已完成"
    },{
        "task":"水库日常巡查",
        "problemType":"电话举报",
        "arranger":"陈超",
        "patrols":"张三",
        "beginTime":"2018-08-26",
        "endTime":"2018-08-27",
        "taskState":"已完成"
    },{
        "task":"水库日常巡查",
        "problemType":"电话举报",
        "arranger":"陈超",
        "patrols":"文湘",
        "beginTime":"2018-08-26",
        "endTime":"2018-08-27",
        "taskState":"已完成"
    }];
    $(".pagination-info i").text(data.length);

    function loadTableData(){
        $("#table1").bootstrapTable("destroy");
        $("#table1").bootstrapTable({
            url:"",             //请求后台的路径
            // ajaxOptions:{
            //     headers: {"authorization": $localStorage("token")||getQueryString("token")}
            // },
            method: 'get',      //请求方式
            striped: false,      //是否显示行间隔色
            showExport: false, 
            exportDataType: "all",
            showLoading: true,
            toolbar: '#toolbar',            //工具按钮用哪个容器
            toolbarAlign: 'left',
            
            pagination: true,               //是否显示分页
            paginationLoop: true,           //是否无限循环
            paginationHAlign: 'right',      //分页位置
            
            sortable: true,                 //是否启用排序
            sortOrder: "asc",               //排序方式
            sidePagination: "client",       //分页方式：client客户端分页，server服务端分页（*）
            pageNumber:1,                   //初始化加载第一页，默认第一页
            pageSize:  5,                   //每页的记录行数（*）
            pageList:  [2, 5, 10, 15],      //可供选择的每页的行数（*）
            // paginationDetailHAlign:' hidden', //

            search:true,                //是否显示表格搜索
            searchOnEnterKey:true,      //是否需要点击enter显示数据
            strictSearch: true,
            showHeader:true,            //是否显示表头
            showColumns: true,          //是否显示所有的列
            showRefresh: true,          //显示刷新按钮
            minimumCountColumns: 2,     //最少允许的列数

            // height: 400,        //行高，如果没有设置height属性，表格自动根据记录条数觉得表格高度
     
            showToggle:true,    //是否显示详细视图和列表
            cardView: false,    //是否显示详细视图
            detailView: true,   //是否显示父子表
            clickToSelect:true, //是否启用点击选中行

            exportDataType: "selected",        //导出checkbox选中的行数

            // paginationFirstText: "首页",
            // paginationPreText: '上一页',
            // paginationNextText: '下一页',
            // paginationLastText: '最后一页',
            
            data:data,
            //得到查询的参数
            // queryParams : function (params) {
            //         //这里的键的名字和控制器的变量名必须一直，这边改动，控制器也需要改成一样的
            //         var temp = {   
            //             rows: params.limit,                         //页面大小
            //             page: (params.offset / params.limit) + 1,   //页码
            //             sort: params.sort,      //排序列名  
            //             sortOrder: params.order //排位命令（desc，asc） 
            //         };
            //         return temp;
            //     },
            columns:[{
                    checkbox: true,  
                    visible: true                  //是否显示复选框  
            },{
                field: 'task',
                title: '任务名称'
            },{
                field: 'problemType',
                title: '问题类型',
                width:'12%'
            },{
                field: 'arranger',
                title: '安排人',
                width:'12%'
            },{
                field: 'patrols',
                title: '巡查人员',
                width:'12%'
            },{
                field: 'beginTime',
                title: '开始时间',
                width:'12%',
                height:'46px'
            },{
                field: 'endTime',
                title: '截止时间',
                width:'12%',
                formatter:function(value,row,index){
                    var html = "";
                    if(index == 3 || index == 7) {
                        var html = '<div class="show-colos">'+value+'</div>';
                    }else {
                        var html = value;
                    }
                    return html;
                }
            },{
                    field: 'taskState',
                title: '任务状态',
                width:'12%',
                formatter:function(value,row,index){
                    var html = "";
                    if(value == "已完成") {
                        var html = '<div class="task-finish"><span class="finish-ico""><i></i>'+value+'</span></div>';
                    }else if(value == "未完成"){
                        var html = '<div class="task-unfinish"><span class="unfinish-ico " onclick="showdetails()"><i></i>'+value+'</span></div>';
                    }
                    return html;
                }
            }],
            onLoadSuccess: function(data){

            },
            onLoadError: function(data){
            }

        });
    }
    loadTableData();
    $('table1').bootstrapTable('refresh'); //删除数据自动更新
</script>

</html>
```

