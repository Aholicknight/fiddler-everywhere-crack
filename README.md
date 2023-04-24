# Get Latest Version

## Linux

api(dot)getfiddler(dot)com/linux/latest-linux

## Windows

api(dot)getfiddler(dot)com/win/latest

## NOTICE

If you are using windows, just try <https://github.com/dnSpyEx/dnSpy>

## get ilasm (ildasm)

1. dotnet new console -n test
2. cd test
3. dotnet add package Microsoft.NETCore.ILAsm (ILDAsm)
4. dotnet publish -c Release --self-contained --runtime linux-x64
5. export PATH=$(pwd)/bin/Release/netcoreapp3.1/linux-x64/publish:$PATH
6. ilasm (ildasm)

## main.xxxx.js

Open the `Fiddler/Resources/APP/OUT/Webserver/ClientApp/Dist/Main.xxx.js`

 Add at the beginning of the function: (please replace the `IE` to the parameter name)

```javascript
Ie.licenseInfo.currentLicense = "Enterprise"
Ie.licenseInfo.hasExpiredTrial = false
Ie.licenseInfo.isTrialAvailable = false
Ie.licenseInfo.hasValidLicense = true
```

## Fiddler.WebUi.il

> Modify this file to remove file verification

 Two functions `TryopenClientMainScript` and`TryopeneletronMainscript`

 Delete all code before the following code

```
IL_0208:  /* 17   |                  */ ldc.i4.1
IL_0209:  /* 2A   |                  */ ret
```

## FiddlerBackendSDK.il

### method FiddlerBackendSDK.User.UserClient::GetBestAccount

Delete IL_000D -IL_0020 corresponding if statement
 Delete IL_003F -IL_0040 corresponding `Return Null;

### method '<>c__DisplayClass18_0'::'<GetBestAccount>b__0'

Delete IL_0000 -IL_0019, insert `ldc.i4.1` before IL_001e (that is, the function body returns directly`true`)

from

```c#
public AccountDTO GetBestAccount(UserWithBestAccountDTO user)
{
 if (user.BestEverywhereAccountId != null)
 {
  return user.Accounts.FirstOrDefault((UserAccountDTO x) => x.Id == user.BestEverywhereAccountId.Value);
 }
 return null;
}
```

to

```c#
public AccountDTO GetBestAccount(UserWithBestAccountDTO user)
{
 return user.Accounts.FirstOrDefault((UserAccountDTO x) => true);
}
```

## Disable update

 Modify the `Fiddler/Resources/APP/OUT/main.js`, search`E.SettingsService.get (). AutopdateSettings.disabled` d`

## Some Detail

[Let me see](./DETAIL.MD)
 
## Exempt statement

 This warehouse is used only for technical learning and communication. If there is a related document, please delete the relevant content within 24 hours after learning.

 Do not use the content of this project for illegal purposes. Users are responsible for any adverse consequences that may produce any adverse consequences when used.

 Any direct or indirect consequences and losses caused by the information provided by this tool is responsible for the user himself, and the author shall not bear any responsibility for this.
