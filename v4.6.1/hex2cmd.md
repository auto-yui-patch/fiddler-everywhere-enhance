## op code

/* 17   |                  */ ldc.i4.1

/* 18   |                  */ ldc.i4.2

/* 2A   |                  */ ret

## Fiddler.WebUi

D:\GitHub\fiddler-everywhere-crack\v4.6.1\Fiddler.WebUi\Fiddler.WebUi.dll

step1: 0x00105FAC 2B 05 -> 2A 00  CheckStub直接return (这里检查Fiddler.WebUi.dll自身是否被修改)

step2: 0x0006D0B2 16 -> 18 main.js检查跳过
```javascript
// 检查main.js的MD5
const isOk = calMd5('main.js')
// 把isOk当成0或1
const t = isOk == 0 // isOk的取值只能是0或1，要让t总是false，就把右边的0换成2
if (t)
{
  // error
  exit()
}
// ok
``` 

step3: 0x0006C7F9 16 -> 18 dist/main.xxx.js检查跳过

## FiddlerBackendSDK

step1: 0x00048270 16 -> 18 自身Hash检查跳过

step2: 0x00012004 2B 05 -> 17 2A    注意：自建服务器可能需要移除此变更
`FirstOrDefault((LicenseSeatDTO x) => x.Id == CS$<>8__locals1.user.BestEverywhereAccountId.Value);` -> `FirstOrDefault((LicenseSeatDTO x) => true);`

step3: 0x00001EEF 3B 47 00 00 00 -> 3B 26 00 00 00 GetBestAccount 注意：自建服务器可能需要移除此变更
       0x00001EF4 38 42 00 00 00 -> 38 21 00 00 00 GetBestAccount 注意：自建服务器可能需要移除此变更

step4: 0x0000C9C4 11 03 -> 17 00 remove the validation of HTTP signature

## main.xxx.js

1. 搜索 `verifyResponse` 处理
2. 删掉这一段：`.then((c) => t.verifyResponse(c?.headers, c?.body))`
