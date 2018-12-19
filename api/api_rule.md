### 协议规则
* * * * *
<table>
<tbody>
  <tr>
    <th width="15%">传输方式</th>
    <td>为保证交易安全性，采用HTTPS传输</td>
  </tr>
  <tr>
    <th>提交方式</th>
    <td>采用POST方法提交</td>
  </tr>
  <tr>
    <th>数据格式</th>
    <td>提交和返回数据都为Json格式，基本数据 {"result_code":"OK","result_msg":"SUCCESS","charge": { }}</td>
  </tr>
  <tr>
    <th>字符编码</th>
    <td>统一采用UTF-8字符编码</td>
  </tr>
  <tr>
    <th>签名算法</th>
    <td>RSA2，后续会兼容SHA1、MD5等。</td>
  </tr>
  <tr>
    <th>签名要求</th>
    <td>请求和接收数据均需要校验签名</td>
  </tr>
  <tr>
    <th>证书要求</th>
    <td>所有API操作都要求使用证书</td>
  </tr>
  <tr>
    <th>判断逻辑</th>
    <td>先判断协议字段返回，再判断业务返回，最后判断交易状态</td>
  </tr>
  </tbody>
</table>

### 参数规范
* * * * *
1、交易金额
交易金额默认为人民币交易，接口中参数支付金额单位为【元】。
2、交易类型
WXSCAN--微信扫码支付、QQSCAN--QQ扫码支付，统一下单接口channel的传参可参考这里
3、货币类型
货币类型的取值列表：
CNY：人民币

### 签名算法
* * * * *
>[success]第一步：设所有发送或者接收到的数据为集合A，将集合M内非空参数值的参数按照参数名`ASCII`码从小到大排序（字典序），使用URL键值对的格式（即key1=value1&key2=value2…）拼接成字符串`string`。
特别注意以下重要规则：
◆ 参数名ASCII码从小到大排序（字典序）；
◆ 如果参数的值为空不参与签名；
◆ 参数名区分大小写；
◆ 验证调用返回或支付中心主动通知签名时，传送的sign参数不参与签名，将生成的签名与该sign值作校验。
◆ 支付中心接口可能增加字段，验证签名时必须支持增加的扩展字段

>[warning]第二步：在`string`最后拼接上`key`得到`stringSignTemp`字符串，并对`stringSignTemp`进行`Base64`运算，再将得到的字符串所有字符转换为大写，得到`sign`值并入RSA进行签名运算得出最后的`signature`。

>商户中心会分配业务系统key，业务系统会有API请求key以及商户公钥`cretKey`：
`key：业务系统请求支付中心对应的key`
`cretKey：支付中心业务系统数据处理Key`

>[danger]示例 ：`RmLCFirMbwv1I9s3Wdq6sTzLYOQrMm/ZlHZFj+oyNToFFJzAx79pG+aCMJ56v81vmtIlCrksvXCyXlW4QqJJGF0HfM23ypB6hK2DWDeIO8irluig7mbx7BjlKPl30yCMejdnIVBYNh2v4oVF+85M2IgsdDpeyWhPofXfyxmKU6ibIr5U+Ir6CNjtvX9PRVSk9PbChmwKNuOzAGRRc0qCLXumD118huaWTa2kKemyInt2CvU6hbxkG0G5Xq0Xt86aduLwGXFzNGVhusb00nQVa44GkzOQ2+4BBQrYFZ1ZY9NQZz/OSgwOcNJ4Q1NY1uQVdL9cHhX15sdYgt2zjxLnwg==`


