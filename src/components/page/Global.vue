<script type="text/javascript">
const serverPath = 'https://apptx.yequandaka.com/app_test'
const roleIdKey = 'role_id'
const codeError = {
  1: '参数错误,数据为空或者类型不对等',
  2: '登录失败,如无此账号或者密码错误等',
  3: '来自post请求中的Body解析json失败'
}
const isChrome = function () {
  let u = navigator.appVersion
  let webKit = u.indexOf('AppleWebKit') > -1
  return webKit
}
const isNumber = function (str) {
  var rs = true
  var re = /^(-?\d+)(\.\d+)?$/
  if (!re.test(str)) {
    rs = false
  }
  return rs
}
const handleSpecialNumber = function (number) {
  var rs = number.toString()
  rs = Number(rs)
  return rs
}
export default{
  serverPath,
  codeError,
  roleIdKey,
  isChrome,
  isNumber,
  handleSpecialNumber
}
</script>
