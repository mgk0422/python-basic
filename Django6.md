

# Django 시각화   

CSV -> model

django - 파일 업로드(.csv)

 django - vistalization(시각화) -script(json)

numpay - pandas -

 script - jquery, d3,google chart,highchart

ajax - 비정형 데이터 - daframe(pandas) - (.csv) - model(class)

---

Ajax (Async Javascript And XML)는 웹 페이지에서 새로운 데이터를 보여주려고 할 때 웹페이지 전체를 새로고침 하지 않고, 보여주고자 하는 데이터가 포함된 페이지의 일부 만을 로드 하기 위한 기법

**Ajax 동작방식**

1. 요청(request) - 브라우저가 서버에 정보를 요청한다.
2. 서버의 동작 - 서버는 JSON, XML 등의 형식으로 데이터를 전달한다.
3. 응답(response) - 브라우저에서 이벤트가 발생하여 콘텐츠를 처리한다.



* ChartApp 생성

```
python manage.py startapp ChartApp
```

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'helloApp',
    'PollsApp',
    'BbsApp',
    'ChartApp', # 추가
]
```

```python
urlpatterns = [
    path('admin/', admin.site.urls),
    path('hello/', include('helloApp.urls')),
    path('polls/', include('PollsApp.urls')),
    path('bbs/',include('BbsApp.urls')),
    path('chart/', include('ChartApp.urls')),  # 추가
]
```

```
def intro(request):
    return render(request,'chart_index.html')
```

```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <ul>
        <a href = "../line"><li>line chart</li></a>
    </ul>
</body>
</html>
```

```python
class Seops(models.Model):
    name =models.CharField(max_length=50)
    img = models.CharField(max_length=50)
    status = models.CharField(max_length=50)

    def __str__(self):
        return self.name+ ",",self.img + "," ,self.status
```



* 꺽은선 그래프 그리기

```python
urlpatterns = [
    path('index/', views.intro, name='index'),
    path('line/', views.line, name='line'),]
```

```python
def line(request):
    seoul = [7.0, 6.9, 9.5, 7.0, 6.9, 9.5, 7.0, 6.9, 9.5, 7.0, 6.9, 9.5]
    london = [8.0, 2.9, 8.6, 7.0, 7.9, 8.5, 7.0, 6.4, 8.5, 6.0, 8.2, 9.2]

    context = {'seoul': seoul,'london': london}
    return render(request,'chart_line.html',context)
```

```python
<chart_line.html>

<script>
        Highcharts.chart('container',{
            chart : { type : 'line'} ,
            title : { text : '처음으로 그리는 웹 차트'},
            subtitle : {text : 'jslim'},
            xAxis : {
                categories : ['1월','2월','3월','4월','5월','6월','7월','8월','9월','10월','11월','12월']
            },
            yAxis : {
                title : {text : '온도'}
            },
            plotOptions : {
            line :{
                dataLabels : { enabled : true }
            },
            enableMouseTracking : true
            },
            series : [
                { name : 'seoul',
                  data : {{seoul}}
                  },
                { name : 'london',
                  data : {{london}}
                  }


            ]
        })
    </script>
```

![image-20200924162816503](C:\Users\mgk04.DESKTOP-8Q51H2D\AppData\Roaming\Typora\typora-user-images\image-20200924162816503.png)





* 막대그래프 그리기

```python
urlpatterns = [
    path('index/', views.intro, name='index'),
    path('line/', views.line, name='line'),
    path('bar/', views.bar, name='bar'),]
```

```python
def bar(request):

    Africa = [107, 31, 635, 203, 2]
    America = [133, 156, 947, 408, 6]
    Asia = [814, 841, 3714, 727, 31]
    Europe = [1216, 1001, 4436, 738, 40]

    context = {'Africa': Africa, 'America': America,'Asia':Asia,'Europe':Europe}
    return render(request,'chart_bar.html', context)
```

```python
<script>
        Highcharts.chart('container', {
          chart: {
            type: 'bar'
          },
          title: {
            text: 'Historic World Population by Region'
          },
          subtitle: {
            text: 'Source: <a href="https://en.wikipedia.org/wiki/World_population">Wikipedia.org</a>'
          },
          xAxis: {
            categories: ['Africa', 'America', 'Asia', 'Europe', 'Oceania'],
            title: {
              text: null
            }
          },
          yAxis: {
            min: 0,
            title: {
              text: 'Population (millions)',
              align: 'high'
            },
            labels: {
              overflow: 'justify'
            }
          },
          tooltip: {
            valueSuffix: ' millions'
          },
          plotOptions: {
            bar: {
              dataLabels: {
                enabled: true
              }
            }
          },
          legend: {
            layout: 'vertical',
            align: 'right',
            verticalAlign: 'top',
            x: -40,
            y: 80,
            floating: true,
            borderWidth: 1,
            backgroundColor:
              Highcharts.defaultOptions.legend.backgroundColor || '#FFFFFF',
            shadow: true
          },
          credits: {
            enabled: false
          },
          series: [{
            name: 'Year 1800',
            data: {{Africa}}
          }, {
            name: 'Year 1900',
            data: {{America}}
          }, {
            name: 'Year 2000',
            data: {{Asia}}
          }, {
            name: 'Year 2016',
            data: {{Europe}}
          }]
        });

    </script>
```

![image-20200924162856313](C:\Users\mgk04.DESKTOP-8Q51H2D\AppData\Roaming\Typora\typora-user-images\image-20200924162856313.png)



* 워드클라우드

```python
urlpatterns = [
    path('index/', views.intro, name='index'),
    path('line/', views.line, name='line'),
    path('bar/', views.bar, name='bar'),
    path('wordcloud/', views.wordcloud, name='wordcloud'),]
```

```python
def wordcloud(request):
    txt = '안녕하세요 저는 귀여운 망고입니다'
    context = {'txt':txt}
    return render (request,'chart_wordcloud.html',context)
```

```python
   <script>
        var text = '{{txt}}'; // 받는 데이터가 문자열일 경우 앞뒤에 '를 붙여 
                              // 문자열로 인식되게 해야한다.
        var lines = text.split(/[,\. ]+/g),
          data = Highcharts.reduce(lines, function (arr, word) {
            var obj = Highcharts.find(arr, function (obj) {
              return obj.name === word;
            });
            if (obj) {
              obj.weight += 1;
            } else {
              obj = {
                name: word,
                weight: 1
              };
              arr.push(obj);
            }
            return arr;
          }, []);

        Highcharts.chart('container', {
          accessibility: {
            screenReaderSection: {
              beforeChartFormat: '<h5>{chartTitle}</h5>' +
                '<div>{chartSubtitle}</div>' +
                '<div>{chartLongdesc}</div>' +
                '<div>{viewTableButton}</div>'
            }
          },
          series: [{
            type: 'wordcloud',
            data: data,
            name: 'Occurrences'
          }],
          title: {
            text: 'Wordcloud of Lorem Ipsum'
          }
        });
    </script>
```



![image-20200924162937928](C:\Users\mgk04.DESKTOP-8Q51H2D\AppData\Roaming\Typora\typora-user-images\image-20200924162937928.png)



* ajax

```python
urlpatterns = [
    path('index/', views.intro, name='index'),
    path('line/', views.line, name='line'),
    path('bar/', views.bar, name='bar'),
    path('wordcloud/', views.wordcloud, name='wordcloud'),
    path('ajax/', views.ajax, name='ajax'),
]
```

```python
def ajax(request):
    return  render(request,'chart_ajax.html')
```

```python
   <script>
        Highcharts.getJSON(
          'https://cdn.jsdelivr.net/gh/highcharts/highcharts@v7.0.0/samples/data/usdeur.json',
          function (data) {

            Highcharts.chart('container', {
              chart: {
                zoomType: 'x'
              },
              title: {
                text: 'USD to EUR exchange rate over time'
              },
              subtitle: {
                text: document.ontouchstart === undefined ?
                  'Click and drag in the plot area to zoom in' : 'Pinch the chart to zoom in'
              },
              xAxis: {
                type: 'datetime'
              },
              yAxis: {
                title: {
                  text: 'Exchange rate'
                }
              },
              legend: {
                enabled: false
              },
              plotOptions: {
                area: {
                  fillColor: {
                    linearGradient: {
                      x1: 0,
                      y1: 0,
                      x2: 0,
                      y2: 1
                    },
                    stops: [
                      [0, Highcharts.getOptions().colors[0]],
                      [1, Highcharts.color(Highcharts.getOptions().colors[0]).setOpacity(0).get('rgba')]
                    ]
                  },
                  marker: {
                    radius: 2
                  },
                  lineWidth: 1,
                  states: {
                    hover: {
                      lineWidth: 1
                    }
                  },
                  threshold: null
                }
              },

              series: [{
                type: 'area',
                name: 'USD to EUR',
                data: data
              }]
            });
          }
        );

    </script>
```



![image-20200924163002061](C:\Users\mgk04.DESKTOP-8Q51H2D\AppData\Roaming\Typora\typora-user-images\image-20200924163002061.png)