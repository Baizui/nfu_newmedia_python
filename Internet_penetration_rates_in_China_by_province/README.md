Internet_penetration_rates_in_China_by_province

英文名字为Internet_penetration_rates_in_China_by_province,中文名字为中国省份互联网普及率。
		
# 简介 
选取省份，输入方面为省份的名称，输出方面则是省份的10年互联网普及率，可查省份34个，数据来源为从国家数据统计局官网取得的tsv档和json档。


		

## 输入：
用户输入省份名称或直辖市名称，交互界面使用到[Html form <select>下拉列表菜单与跳转菜单表单标签篇-DIVCSS5](http://www.divcss5.com/html/h336.shtml)，所以用户可以用省份名称或直辖市名称找到所需的数据。详细见[templates/entry.html](templates/entry.html)
## 输出：
[该省份互联网普及率最近十年的数据](https://github.com/Baizui/nfu_newmedia_python/blob/master/province/templates/results.html)
## 从输入到输出，本组作品使用了：
### 模块
* pandas 大数据，将数据转化为tsv档,再将它转为字典。弄成列表，将每个省份与十年数据对接起来。
* requests
* json
### 数据,
* [国家数据统计局官网](http://data.stats.gov.cn/easyquery.htm?cn=E0103),本组并未使用API

## Web App动作描述

1.以下按web 请求（web request） - web 响应 时序说明

2.後端伺服器启动：执行 Internet_penetration_rates_in_China_by_province.py 启动後端伺服器，等待web 请求。启动成功应出现： * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)

3.前端浏览器web 请求：访问 http://127.0.0.1:5000/ 启动前端web 请求

4.後端伺服器web 响应：Internet_penetration_rates_in_China_by_province.py 中 执行 了@app.route('/') 下的 entry_code()函数，以HTML模版[templates/entry.html](templates/entry.html)及一个含省份名称的列表（见代码 the_user_province=list_province）产出的产生《欢迎来到网上省份互联网普及率搜索！》的HTML页面

5.前端浏览器收到web 响应：出现HTML页面有HTML表单的输入，变数名称(name)为'province'，使用了HTML5的select 定义在 name='province' 及 select标签，详见HTML模版[templates/entry.html](templates/entry.html)

6.前端浏览器web 请求：用户选取指标後按了提交钮「跑吧」，则产生新的web 请求，按照form元素中定义的method='POST' action='/search_province'，以POST为方法，动作为/search_province的web 请求

7.後端服务器收到用户web 请求，匹配到@app.route('/search_province', methods=['POST'])的函数 do_search()

8.[Internet_penetration_rates_in_China_by_province.py](Internet_penetration_rates_in_China_by_province.py) 中 def do_search() 函数，把用户提交的数据，以flask 模块request.form['province']	取到Web 请求中，HTML表单变数名称province的值，存放在province这Python变数下，再使用flask模块render_template 函数以[templates/results.html](templates/results.html)模版为基础（输出），其中模版中the_province的值，用province这变数之值，其他10项值如此类推。

9.前端浏览器收到web 响应：模版中[templates/results.html](templates/results.html) 的变数值正确的产生的话，前端浏览器会收到正确响应，看到省份的互联网普及率。

## 作者成员：
见[_team_.tsv](_team_/_team_.tsv)


		
