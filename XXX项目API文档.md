#XXX项目API文档
##校验规则
1. 请求参数除sign字段组成数组并按照参数字母序排序
2. 使用`http_build_query`组装成形如:`key1=val1&key2=val2`
3. 第2步组装的字符串连接API_KEY并md5
4. 第3步所得md5结果`strtoupper`
5. 第4不所得字符与sign参数比较

##返回格式
json
##错误码列表
|CODE|DESC|
|-------|-------|
|-1|错误|
|0|正确|
|1|sign错误|
|2|接口超时|
|3|IP白名单|
##登录API
###请求方式
GET
###接口地址
http://path/to/your/api/login
### 参数列表
|字段|说明|样例|
|------|---|---|
|account|账号|abc|
|ts|unix时间戳单位（秒）||
|sign|校验串|ABCSDFASFASWERS123SFDFSDSDF|
###返回字段
* 样例

`{
    "code": 0,
    "msg": "",
    "response":{
           "key1":"val1",
           "key2":"val2"
    }
 }`
* 字段说明

|字段|说明|
|---|---|
|key1|xxx|
|key2|xxx|
###代码示例
* PHP

`$params = array(
      'key1'=>val1,
      'key2'=>val2,
      'ts'=>time()
);
ksort($params);
$params['sign'] = md5(http_build_query($params).API_KEY);
$url = $login_url.'?'.http_build_query($params);
$response = http_query($url);
$response = json_decode($response,true);`

