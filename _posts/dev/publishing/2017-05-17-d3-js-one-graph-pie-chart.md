---
layout: post
comments: true
date: 2017-05-17 16:32:00
title: "D3.js 사용법 및 차트 만들기"
description: "D3.js 원 그래프와 파이차트 만들기"
subject: dev
categories: [ publishing ]
sub: [ jQuery, html ]
tags: [ js, jQuery, d3, chart, graph ]
---

<div class="list-of-tables"><p>목차</p></div>

## 1. 사전준비<a id="1-사전준비" href="#1-사전준비" class="s-link" aria-hidden="true"></a>

<https://d3js.org/>{: target="_blank"} D3 홈페이지로 접속합니다.

다운로드를 받거나, 스크립트를 추가해서 사용할 수 있습니다.

```javascript
<script src="https://d3js.org/d3.v4.min.js"></script>
```

홈페이지를 참고하면 더 많은 정보를 얻을 수 있지만 ..

영어 싫어 ㅠㅠ 라고 외치는 저는 블로그를 참고 합니다 ... (?)

중간단계 건너 뛰실 분들은 요기 클릭해주세요 -> [완성작 보러가기](#4-그냥-완성해버리기)

[참고 블로그](#참고-블로그)

## 2. 원 그래프 만들기<a id="2-원-그래프-만들기" href="#2-원-그래프-만들기" class="s-link" aria-hidden="true"></a>

블로그 글이 2014년도 여서 버전이 바뀌는 바람에 에러가 나더라구요 ㅠ_ㅠ

이럴땐 우리모두의 사랑 stackoverflow !!

간단한 원 그래프부터 만들어 보아요 :)

div.graph 에 작업할게요.

### 2-1. 기본 원 그래프 만들기<a id="2-1-기본-원-그래프-만들기" href="#2-1-기본-원-그래프-만들기" class="s-link" aria-hidden="true"></a>

```html
# html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="utf-8">
</head>
<body>
    <div class="graph"></div>
    <script src="https://d3js.org/d3.v4.min.js"></script>
    <script src="/js/d3_app.js"></script>
</body>
</html>
```

```javascript
# javascript
// 250x250 의 <svg id="graphWrap"></svg> 를 div.graph 에 추가
var w = 250, h = 250;
d3.select(".graph")
    .append("svg")
    .attr("width", w)
    .attr("height", h)
    .attr("id", "graphWrap");
var graphWrap = d3.select("#graphWrap");

// 그래프 데이터 // 합쳐서 100이 아니더라도 원이 생성됨
var graphData = [15, 25, 60];
// pie 생성
// var pie = d3.layout.pie(); // d3 v3 버전
var pie = d3.pie();
// 안쪽 반지름, 바깥쪽 반지름 설정 // 200x200 의 원 그래프 생성
// var arc = d3.svg.arc().innerRadius(0).outerRadius(100); // d3 v3 버전
var arc = d3.arc().innerRadius(0).outerRadius(100);

// 원 그리기
var oneGraph = graphWrap.selectAll("path").data(pie(graphData));
// 데이터 추가
oneGraph.enter() // 데이터 수 만큼 반복
    .append("path")
    .attr("class", "pie") // 클래스 추가
    .attr("d", arc) // 부채꼴 지정
    .attr("fill", "yellow")
    .attr("stroke", "black")
    .attr("transform", "translate("+(w/2)+","+(h/2)+")");
```

<div class="graph_1"></div>

### 2-2. 원 그래프 배경색 변경<a id="2-2-원-그래프-배경색-변경" href="#2-2-원-그래프-배경색-변경" class="s-link" aria-hidden="true"></a>

`oneGraph.enter()` 부분만 수정해주세요.

```javascript
# javascript
// 데이터 추가
oneGraph.enter()
    .append("path")
    .attr("class", "pie")
    .attr("d", arc)
    // .attr("stroke", "black")
    .attr("transform", "translate("+(w/2)+","+(h/2)+")")
    .style("fill", function(d, i) {
        return ["red", "orange", "yellow"][i];
    }
);
```

<div class="graph_2"></div>

### 2-3. 원 그래프 애니메이션<a id="2-3-원-그래프-애니메이션" href="#2-3-원-그래프-애니메이션" class="s-link" aria-hidden="true"></a>

`oneGraph.enter()` 부분만 수정해주세요.

```javascript
# javascript
// 데이터 추가
oneGraph.enter()
    .append("path")
    .attr("class", "pie") // 클래스 추가
    // .attr("d", arc) // 부채꼴 지정
    // .attr("stroke", "black")
    .attr("transform", "translate("+(w/2)+","+(h/2)+")")
    .style("fill", function(d, i) {
        return ["red", "orange", "yellow", "blue", "purple"][i];
    })
    .transition()
    .duration(1000)
    .delay(function(d, i) {
        return i * 1000;
    })
    .attrTween("d", function(d, i) {
        var interpolate = d3.interpolate(
            {startAngle : d.startAngle, endAngle : d.startAngle},
            {startAngle : d.startAngle, endAngle : d.endAngle}
        );
        return function(t){
            return arc(interpolate(t));
        }
    });
```

<div class="graph_3"></div>

## 3. 파이차트 만들기<a id="3-파이차트-만들기" href="#3-파이차트-만들기" class="s-link" aria-hidden="true"></a>

아까 설정한 반지름을 조정해주면 됩니다 !!!

`var arc = d3.arc().innerRadius(40).outerRadius(100);` 부분을 참고해주세요.

```javascript
# javascript
var w = 250, h = 250;
d3.select(".graph")
    .append("svg")
    .attr("width", w)
    .attr("height", h)
    .attr("id", "graphWrap");
var graphWrap = d3.select("#graphWrap");

var graphData = [50, 30, 12, 5, 3];
var pie = d3.pie();
var arc = d3.arc().innerRadius(40).outerRadius(100);

var oneGraph = graphWrap.selectAll("path").data(pie(graphData));
oneGraph.enter()
    .append("path")
    .attr("class", "pie") // 클래스 추가
    // .attr("d", arc) // 부채꼴 지정
    // .attr("stroke", "black")
    .attr("transform", "translate("+(w/2)+","+(h/2)+")")
    .style("fill", function(d, i) {
        return ["red", "orange", "yellow", "blue", "purple"][i];
    })
    .transition()
    .duration(1000)
    .delay(function(d, i) {
        return i * 1000;
    })
    .attrTween("d", function(d, i) {
        var interpolate = d3.interpolate(
            {startAngle : d.startAngle, endAngle : d.startAngle},
            {startAngle : d.startAngle, endAngle : d.endAngle}
        );
        return function(t){
            return arc(interpolate(t));
        }
    });
```

<div class="graph_4"></div>

## 4. 그냥 완성해버리기<a id="4-그냥-완성해버리기" href="#4-그냥-완성해버리기" class="s-link" aria-hidden="true"></a>

> 원래 블로그 참고했는데 예전버전이라 뭔가 잘 안돼서 다시 구글링 후 작성 (...)

```html
# html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="utf-8">
</head>
<body>
    <div class="one-graph"></div>
    <script src="https://d3js.org/d3.v4.min.js"></script>
    <script src="/js/d3_app.js"></script>
</body>
</html>
```

```javascript
# javascript
var w = 250, h = 250;
var graphData = [50, 30, 12, 5, 3];
var colorData = ["red", "orange", "yellow", "blue", "purple"];
var pie = d3.pie();
var arc = d3.arc().innerRadius(40).outerRadius(100);

var svg = d3.select(".one-graph")
    .append("svg")
    .attr("width", w)
    .attr("height", h)
    .attr("id", "graphWrap");

var g = svg.selectAll(".pie")
    .data(pie(graphData))
    .enter()
    .append("g")
    .attr("class", "pie")
    .attr("transform","translate("+w/2+","+h/2+")");

// path 태그로 차트에 색을 넣기
g.append("path")
    // .attr("d", arc) // 미리 색을 칠해놓음
    .style("fill", function(d, i) {
        return colorData[i];
    }) // 애니메이션이 싫을경우 arc 를 활성화시키고 아래내용을 주석
    .transition()
    .duration(400)
    .delay(function(d, i) { // 그릴 원 그래프의 시간을 어긋나게 표시
        return i * 400;
    })
    .attrTween("d", function(d, i) { // 보간 처리
        var interpolate = d3.interpolate(
            {startAngle : d.startAngle, endAngle : d.startAngle}, // 각 부분의 시작 각도
            {startAngle : d.startAngle, endAngle : d.endAngle} // 각 부분의 종료 각도
        );
        return function(t){
            return arc(interpolate(t)); // 시간에 따라 처리
        }
    });

// text 태그로 배열 값 넣기
g.append("text")
    .attr("transform", function(d) { return "translate(" + arc.centroid(d) + ")"; })
    .attr("dy", ".35em")
    .style("text-anchor", "middle")
    .text(function(d, i) {
        return graphData[i] + "%";
    });

// text 정 중앙에 텍스트 넣기
svg.append("text")
    .attr("class", "total")
    .attr("transform", "translate("+(w/2-35)+", "+(h/2+5)+")")
    .text("합계:" + d3.sum(graphData));
```

<div class="graph_5"></div>

## 참고 블로그<a id="참고-블로그" href="#참고-블로그" class="s-link" aria-hidden="true"></a>

- DGMong LAB 님 블로그 <http://blog.naver.com/sol9501/220199577721>

<script src="https://d3js.org/d3.v4.min.js"></script>
<script>
// 1번째
var w = 250, h = 250;
d3.select(".graph_1")
    .append("svg")
    .attr("width", w)
    .attr("height", h)
    .attr("id", "graphWrap_1");
var graphWrap_1 = d3.select("#graphWrap_1");

var graphData = [50, 30, 12, 5, 3];
var pie_1 = d3.pie();
var arc_1 = d3.arc().innerRadius(0).outerRadius(100);

var oneGraph_1 = graphWrap_1.selectAll("path").data(pie_1(graphData));
oneGraph_1.enter()
    .append("path")
    .attr("class", "pie_1")
    .attr("d", arc_1)
    .attr("fill", "yellow")
    .attr("stroke", "black")
    .attr("transform", "translate("+(w/2)+","+(h/2)+")");

// 2번째
d3.select(".graph_2")
    .append("svg")
    .attr("width", w)
    .attr("height", h)
    .attr("id", "graphWrap_2");
var graphWrap_2 = d3.select("#graphWrap_2");

var pie_2 = d3.pie();
var arc_2 = d3.arc().innerRadius(0).outerRadius(100);

var oneGraph_2 = graphWrap_2.selectAll("path").data(pie_2(graphData));
oneGraph_2.enter()
    .append("path")
    .attr("class", "pie_2")
    .attr("d", arc_2)
    .attr("transform", "translate("+(w/2)+","+(h/2)+")")
    .style("fill", function(d, i) {
        return ["red", "orange", "yellow", "blue", "purple"][i];
    }
);

// 3번째
d3.select(".graph_3")
    .append("svg")
    .attr("width", w)
    .attr("height", h)
    .attr("id", "graphWrap_3");
var graphWrap_3 = d3.select("#graphWrap_3");

var pie_3 = d3.pie();
var arc_3 = d3.arc().innerRadius(0).outerRadius(100);

var oneGraph_3 = graphWrap_3.selectAll("path").data(pie_3(graphData));
oneGraph_3.enter()
    .append("path")
    .attr("class", "pie_3")
    .attr("transform", "translate("+(w/2)+","+(h/2)+")")
    .style("fill", function(d, i) {
        return ["red", "orange", "yellow", "blue", "purple"][i];
    })
    .transition()
    .duration(1000)
    .delay(function(d, i) {
        return i * 1000;
    })
    .attrTween("d", function(d, i) {
        var interpolate = d3.interpolate(
            {startAngle : d.startAngle, endAngle : d.startAngle},
            {startAngle : d.startAngle, endAngle : d.endAngle}
        );
        return function(t){
            return arc_3(interpolate(t));
        }
    });

// 4번째
d3.select(".graph_4")
    .append("svg")
    .attr("width", w)
    .attr("height", h)
    .attr("id", "graphWrap_4");
var graphWrap_4 = d3.select("#graphWrap_4");

var pie_4 = d3.pie();
var arc_4 = d3.arc().innerRadius(40).outerRadius(100);

var oneGraph_4 = graphWrap_4.selectAll("path").data(pie_4(graphData));
oneGraph_4.enter()
    .append("path")
    .attr("class", "pie_4")
    .attr("transform", "translate("+(w/2)+","+(h/2)+")")
    .style("fill", function(d, i) {
        return ["red", "orange", "yellow", "blue", "purple"][i];
    })
    .transition()
    .duration(1000)
    .delay(function(d, i) {
        return i * 1000;
    })
    .attrTween("d", function(d, i) {
        var interpolate = d3.interpolate(
            {startAngle : d.startAngle, endAngle : d.startAngle},
            {startAngle : d.startAngle, endAngle : d.endAngle}
        );
        return function(t){
            return arc_4(interpolate(t));
        }
    });

var graphData = [50, 30, 12, 5, 3];
var colorData = ["red", "orange", "yellow", "blue", "purple"];
var pie = d3.pie();
var arc = d3.arc().innerRadius(40).outerRadius(100);

var svg = d3.select(".graph_5")
    .append("svg")
    .attr("width", w)
    .attr("height", h)
    .attr("id", "graphWrap");

var g = svg.selectAll(".pie")
    .data(pie(graphData))
    .enter()
    .append("g")
    .attr("class", "pie")
    .attr("transform","translate("+w/2+","+h/2+")");

// path 태그로 차트에 색을 넣기
g.append("path")
    // .attr("d", arc) // 미리 색을 칠해놓음
    .style("fill", function(d, i) {
        return colorData[i];
    }) // 애니메이션이 싫을경우 arc 를 활성화시키고 아래내용을 주석
    .transition()
    .duration(400)
    .delay(function(d, i) { // 그릴 원 그래프의 시간을 어긋나게 표시
        return i * 400;
    })
    .attrTween("d", function(d, i) { // 보간 처리
        var interpolate = d3.interpolate(
            {startAngle : d.startAngle, endAngle : d.startAngle}, // 각 부분의 시작 각도
            {startAngle : d.startAngle, endAngle : d.endAngle} // 각 부분의 종료 각도
        );
        return function(t){
            return arc(interpolate(t)); // 시간에 따라 처리
        }
    });

// text 태그로 배열 값 넣기
g.append("text")
    .attr("transform", function(d) { return "translate(" + arc.centroid(d) + ")"; })
    .attr("dy", ".35em")
    .style("text-anchor", "middle")
    .text(function(d, i) {
        return graphData[i] + "%";
    });

// text 정 중앙에 텍스트 넣기
svg.append("text")
    .attr("class", "total")
    .attr("transform", "translate("+(w/2-35)+", "+(h/2+5)+")")
    .text("합계:" + d3.sum(graphData));
</script>
