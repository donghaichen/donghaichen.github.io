# Bing 每日图片和故事 API 接口

### 图片API地址
```bash
https://cn.bing.com/HPImageArchive.aspx?format=js&idx=0&n=1
参数:
 *  format 格式。我理解为输出格式，不存在或者不等于js，即为xml格式，等于js时，输出json格式；
 *  fidx  时间 表示是显示当天的时间,支持(0-15)
 *  fn  数量限制。最多输出8条
```
 
### 故事API地址
```bash
https://cn.bing.com/cnhp/coverstory?d=20181211
参数:
 * d 日期 格式 年月日 (d的值可选范围：20140501-至今)
```
