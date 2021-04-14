### 已完成部分

* Python数据分析
  * 读取csv文件，将多个csv文件合并成一个文件
    遇到的问题：数据存在NaN,在合并时要对NaN值进行处理（已解决）
```
# 合并数据
result1 =               pd.concat([DateTime,Temperature_N1_301_1,Humidity_N1_301_1,Pressure_N1_301_1,Light_N1_301_1],axis = 1)
result = result.merge(result1,how = 'outer')
```

  * 对csv文件中的时间缺失值补齐

    遇到的问题：产生完整的时间序列后，进行时间缺失值补齐时存在重复值，要**删除重复值**  （已解决）
    
```

# 生成完整时间序列
pdates = pd.date_range(start = df_date.index[0], end = df_date.index[-1],freq='10min')
# 删除重复值
df_date = df_date[~df_date.index.duplicated()]

```

  * 将csv文件数据进行分类处理，并用matplotlib库绘图展示

​       遇到的问题：未过滤数据中的异常值，导致画出的图有点奇怪，暂时只实现判断语句过滤异常值 （ o ）

```
# 湿度
Humidity = Humidity[Humidity <= 80]
plt.plot(pdates,Humidity)
plt.show()
```
<img src = './img/Humidity.jpg'  >

```
# 光照
Light = Answer.loc[:,Title[11:20]]
plt.plot(pdates,Light)
plt.show()
```
<img src = './img/Light.jpg'  >

```
# 大气压
Pressure = Answer.loc[:,Title[21:30]]
Pressure = Pressure[Pressure>800]
plt.plot(pdates,Pressure)
plt.show()

```
<img src = './img/Pressure.jpg'  >

```
# 温度
Temperature = Answer.loc[:,Title[31:40]]
Temperature = Tempture[Temperature <= 40]
plt.plot(pdates,Temperature)
plt.show()
```
<img src = './img/Temperature.jpg'  >