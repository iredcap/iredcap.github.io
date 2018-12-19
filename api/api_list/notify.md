### 应用场景
***
支付完成后，`支付中心`会把相关支付结果和相关信息发送给商户，商户需要接收处理，并返回应答。对后台通知交互时，如果支付中心收到商户的应答不是成功或超时，支付中心则认为通知失败，会在一定的策略定期重新发起通知，尽可能提高通知的成功率，但不保证通知最终能成功。 （通知频率为`15/15/30/180/1800/1800/1800/1800/3600`，单位：`秒`）

>[warning]注意：同样的通知可能会多次发送给商户系统。商户系统必须能够正确处理重复的通知。推荐的做法是，当收到通知进行处理时，首先检查对应业务数据的状态，判断该通知是否已经处理过，如果没有处理过再进行处理，如果处理过直接返回结果成功。在对业务数据进行状态检查和处理之前，要采用数据锁进行并发控制，以避免函数重入造成的数据混乱。

>[danger]特别提醒：商户系统对于支付结果通知的内容一定要做签名验证,并校验返回的订单金额是否与商户侧的订单金额一致，防止数据泄漏导致出现“假通知”，造成资金损失。

### 接口链接
***
统一下单接口提交的参数`notify_url`设置，如果无法访问链接，您的业务系统将无法接收到支付中心的通知。

### 通知参数
***
<table>
      <tbody><tr>
        <th class="name">字段名</th>
        <th class="var">变量名</th>
        <th class="require">必填</th>
        <th class="type">类型</th>
        <th class="example">示例值</th>
        <th class="description">描述</th>
      </tr>
     <tr>
    <td>返回状态码 </td>
    <td>return_code </td>
    <td>是 </td>
    <td>String(16) </td>
    <td>SUCCESS</td>
    <td>
        <p>SUCCESS</p>
</td>
</tr>
<tr>
    <td>返回信息 </td>
    <td>return_msg </td>
    <td>是</td>
    <td>String(128) </td>
    <td>OK</td>
  <td>OK</td>
</tr>
</tbody>
</table>


>以下在成功返回是的通知数据

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
