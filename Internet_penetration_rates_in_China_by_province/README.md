Internet_penetration_rates_in_China_by_province

英文项目名称为Internet_penetration_rates_in_China_by_province,中文名字为中国省份互联网普及率.就是指各省份或者直辖市的十年互联网普及率相关数据的说明.
		
# 简介 
中国各省份或直辖市十年互联网普及率的查询（十年即2006年~2015年）,输入方面用户可输入想查询省份或直辖市的名称（如"广东省"、"北京市")，输出方面则是该省份或者直辖市的10年互联网普及率（由于前四年的数据空白,只有后六年的数据）,可查省份和直辖市一共34个.数据来源为从[国家数据统计局官网](http://data.stats.gov.cn/easyquery.htm?cn=E0103)取得的tsv档和json档.


		

## 输入：
用户输入省份名称或直辖市名称,交互界面使用到[HTML5之select表单标签](http://www.divcss5.com/html/h336.shtml),所以用户可以用省份名称或直辖市名称找到所需的数据.详细见[templates/entry.html](templates/entry.html)
## 输出：
用户得到的输出结果为：该省份或者直辖市的十年互联网普及率的数据,详细见[templates/results.html](templates/results.html)


## 从输入到输出,除了flask模块,本组作品使用了：

### 模块
* [requests](http://docs.python-requests.org/zh_CN/latest/user/quickstart.html)
* [json](https://docs.python.org/2/library/json.html)
* [pandas](http://stackoverflow.com/questions/22180993/pandas-dataframe-display-on-a-webpage)
### 数据
*  从 [国家数据统计局官网](http://data.stats.gov.cn/easyquery.htm?cn=E0103)上，将34个省份和直辖市的资料保存到本地，见[data](data)
*  资料类型：字典包字典,tsv档和json档.
### API
*  本组未使用API,使用了pandas大数据分析，详细见[main.py](main.py)
*  数据清理：各个省份或者直辖市有各自的代码以做文件名称的json档，方便调用.详细见[province_code_name.json ](province_code_name.json )

## Web App动作描述

以下是web请求前的准备工作

1.在[main.py](main.py)中,pd.DataFrame.from()函数，未调用api，生成一个含有所有省份和直辖市简要资料的tsv档[fsnd_data.tsv](fsnd_data.tsv)保存到本地的[data](data)文件夹中。pd.DataFrame.from()函数，读取[fsnd_data.tsv](fsnd_data.tsv)并返回省份或直辖市简要资料的字典。用pd.DataFrame.from函数()，调用大数据pandas(pd.DataFrame.from)，以集合推导的方式，建立以code号为键，省份中文名为值的小字典to_dict(见代码 data_list = [v for k,v in data.items()])。跑含有code号的省份或者直辖市 , 并把每个code号下的省份或者直辖市以其中文code为文件名，输成json档  [province_code_name.json](  province_code_name.json  )  ，最终结果为34个省份或者直辖市，保存到本地的[data](data)文件夹中。

2.在[datatemp.py ](datatemp.py )中，def get_data()函数，打开[province_code_name.json ](province_code_name.json )，返回一个以省份或者直辖市的代码为键，中文名和代码为值的字典(见代码temp = df[['reg','sj','data']].set_index('reg').to_dict()['data'])，用做后面的函数和网页的表单界面，目标是用户输入英省份或者直辖市的中文名能得到想要的结果。def get_data()函数，将省份的中文名输入转换成互联网普及率，调用函数def get_data()，运用for循环，如（int_pr = df.query("zb=='A0G0H05'")[['reg','sj', 'data']]）,从中可以得到该省份或者直辖市的代码、时间、数据.如果输入的名称不存在,返回'error'字符串.

* 以下按web 请求（web request） - web 响应 时序说明

1.后端伺服器启动：执行 game_hero_data.py 启动后端伺服器，等待web 请求。启动成功应出现： * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)

2.前端浏览器web 请求：访问 http://127.0.0.1:5000/ 启动前端web 请求

3.後端伺服器web 响应：[Internet_penetration_rates_in_China_by_province.py](Internet_penetration_rates_in_China_by_province.py) 中 执行 了@app.route('/') 下的 entry_code()函数，以HTML模版[templates/entry.html](templates/entry.html)及一个含省份名称的列表（见代码 the_user_province=list_province）产出的产生《欢迎来到网上省份互联网普及率搜索！》的HTML页面

4.前端浏览器收到web 响应：出现HTML页面有HTML表单的输入，变数名称(name)为'select name='province''，使用了HTML5的select 定义在 name='province' 及 select标签，详见HTML模版[templates/entry.html](templates/entry.html)

5.前端浏览器web 请求：用户选取指标後按了提交钮「跑吧」，则产生新的web 请求，按照form元素中定义的method='POST' action='/search_province'，以POST为方法，动作为/search_province的web 请求

6.後端服务器收到用户web 请求，匹配到@app.route('/search_province', methods=['POST'])的函数 do_search()

7.[Internet_penetration_rates_in_China_by_province.py](Internet_penetration_rates_in_China_by_province.py)文件调用到[main.py](main.py) 中 pd.DataFrame.from() 等函数，把用户提交的数据，以flask 模块request.form['/search_province']	取到Web 请求中，并放到函数的参数中运行得到输出数据，再使用flask模块render_template 函数以[templates/results.html](templates/results.htm)模版为基础（输出），其中模版中the_province的值，用results = get_data(int(code))这变数之值，其他10项值如此类推。

8.前端浏览器收到web 响应：模版中[templates/results.html](templates/results.html) 的变数值正确的产生的话，前端浏览器会收到正确响应，看到指标的相关元数据。

## 作者成员：
见[_team_.tsv](_team_/_team_.tsv)


		
