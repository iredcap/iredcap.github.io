### 接口链接
* * * * *
URL地址：https://api.iredcap.cn/pay/orderquery
**注意：** 此接口为测试接口，一切以搭建为主

### 请求参数
* * * * *
<table>
    <thead>
        <tr>
        <th style="width: 120px;">字段名</th>
        <th style="width: 120px;">变量名</th>
        <th style="width: 100px;">类型</th>
        <th style="width: 80px;">必填</th>
        <th style="width: 160px;">示例值</th>
        <th style="width: 240px;">说明</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <td>商户UID</td>
            <td>mchid</td>
            <td>string</td>
            <td>True</td>
            <td>100001</td>
            <td>商户平台注册UID</td>
        </tr>
        <tr>
            <td>商户订单号</td>
            <td>out_trade_no</td>
            <td>string</td>
            <td>True</td>
            <td>1009660380201506130</td>
            <td>商户订单号</td>
        </tr>
        <tr>
            <td>随机参数</td>
            <td>nonce_str</td>
            <td>string</td>
            <td>True</td>
            <td>o2RvowOHGyfcklTodrNbceaDqo</td>
            <td>随机字符串，不长于32位</td>
        </tr>
        <tr>
            <td>数据签名串</td>
            <td>sign</td>
            <td>string</td>
            <td>True</td>
            <td>RmLCFi1NY1u······dYgt2zjxLnwg==</td>
            <td>通过签名算法计算得出的签名值</td>
        </tr>
        <tr>
            <td>签名方式</td>
            <td>sign_type</td>
            <td>string</td>
            <td>False</td>
            <td>RSA2</td>
            <td>签名类型，目前支持RSA2和MD5，默认为MD5</td>
        </tr>
        </tbody>
    </table>


### 返回数据
* * * * *
<table>
    <thead>
    <tr>
        <th style="width: 120px;">字段名</th>
        <th style="width: 120px;">变量名</th>
        <th style="width: 100px;">类型</th>
        <th style="width: 80px;">必填</th>
        <th style="width: 160px;">示例值</th>
        <th style="width: 240px;">说明</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>返回码</td>
        <td>result_code</td>
        <td>string</td>
        <td>True</td>
        <td>OK</td>
        <td>结果码, OK:成功; 其他:失败</td>
    </tr>
    <tr>
        <td>返回消息</td>
        <td>result_msg</td>
        <td>string</td>
        <td>True</td>
        <td>SUCCESS</td>
        <td>提示信息,SUCCESS:成功</td>
    </tr>
    <tr>
        <td>数据对象</td>
        <td>charge</td>
        <td>object</td>
        <td>True</td>
        <td></td>
        <td>返回支付对象（请看下方具体数据）</td>
    </tr>
    </tbody>
</table>

### 返回结果
* * * * *
>[success] 这里是**成功返回信息**
> 在返回JSON数据中 **result_code=OK** 和 **result_msg= SUCCESS** 时才有  _**charge**_
```
{
    "result_code": "OK",
    "result_msg": "SUCCESS",
    "charge": {
   }
}
```
>[danger] 这里是**错误返回信息**
> 在返回错误数据中仅有 **error_code** 和 **error_msg**
```
{
    "error_msg": "Invalid Request.[ Request header [authentication] Failure.]",
    "error_code": 400000
}
```

