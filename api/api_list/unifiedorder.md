### 业务说明
* * * * *
统一下单接口，商户系统先调用该接口在微信支付服务后台生成预支付交易单

### 业务流程
* * * * *
![业务流程](../../images/attach_14dbae7b7477ca11.png)

### 接口链接
* * * * *
URL地址：https://api.iredcap.cn/pay/unifiedorder
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
            <td>appid</td>
            <td>string</td>
            <td>True</td>
            <td>100001</td>
            <td>商户UID</td>
        </tr>
        <tr>
            <td>商品描述</td>
            <td>subject</td>
            <td>string</td>
            <td>True</td>
            <td>会员充值</td>
            <td>商品简单描述</td>
        </tr>
        <tr>
            <td>商品信息</td>
            <td>body</td>
            <td>string</td>
            <td>True</td>
            <td>会员充值</td>
            <td>支付商品信息</td>
        </tr>
        <tr>
            <td>支付金额</td>
            <td>amount</td>
            <td>bigint</td>
            <td>True</td>
            <td>1000</td>
            <td>支付总金额</td>
        </tr>
        <tr>
            <td>附加数据</td>
            <td>extra</td>
            <td>string</td>
            <td>True</td>
            <td></td>
            <td>附加参数</td>
        </tr>
        <tr>
            <td>支付产品</td>
            <td>channel</td>
            <td>string</td>
            <td>True</td>
            <td>WXSCAN</td>
            <td>支付方式,当前支持: WXSCAN,QQSCAN,AWEB,AWAP</td>
        </tr>
        <tr>
            <td>货币代码</td>
            <td>currency</td>
            <td>string</td>
            <td>True</td>
            <td>CNY</td>
            <td>支付币种,当前支持: CNY</td>
        </tr>
        <tr>
            <td>终端IP</td>
            <td>client_ip</td>
            <td>string</td>
            <td>True</td>
            <td>127.0.0.1</td>
            <td>发起支付IP</td>
        </tr>
        <tr>
            <td>通知地址</td>
            <td>notify_url</td>
            <td>string</td>
            <td>True</td>
            <td></td>
            <td>异步通知地址</td>
        </tr>
        <tr>
            <td>回调地址</td>
            <td>return_url</td>
            <td>string</td>
            <td>True</td>
            <td></td>
            <td>同步回调地址</td>
        </tr>
        </tbody>
    </table>

>[warning] extra参数说明

当请求参数channelId = WXJS（微信公众号支付）时，openId参数必填，对应用户所在微信公众号的openId。
```
{"openId":"wx_o2RvowOHGyfcklTodrNbceaDqo"}
```
### 返回参数
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
        <td>错误码</td>
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
        "channel": "wx_scan",
        "order_no": "A20180924175446924770",
        "client_ip": "112.116.253.55",
        "amount": "100",
        "currency": "CNY",
        "subject": "API支付测试",
        "body": "API支付测试",
        "extra": {
            "openid": "ow_eHIGfsQM6qGrd27qRj3v1R5fyY2PjJ0h"
        },
        "credential": {
            "prepay_id": "wx241754525235056fc4574b7d2697455231",
            "order_qr": "weixin://wxpay/bizpayurl?pr=xxxxxx"
        }
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
