# 前

 The software knows, does not explain;

 The author uses the Linux operating system, so tools such as DNSPY, Reflexil cannot be used (maybe I did not find related visualization tools),

 Therefore, it is treated with Avaloniailspy + ILasm / ILDASM;

 The Classic version does not support Linux, so this modification is made.

# Pre -processing

 Prepare `iLDASM` and`iLasm`

 Use `iLDASM`

 Use `iLDASM`

## Linux Get ILasm (ILDASM)

 1. Install the dotnet, open a empty folder and execute the follow -up command
 2. Dotnet New Console -n test
 3. CD test
 4. Dotnet Add Package Microsoft.netcore.ilasm (ILDASM)
 5. Dotnet Publish -C Release-Self-Contained-Runtime Linux-X64
 6. Export Path = $ (pwd) /bin/release/netcoreapp3.1/linux-x64/publish: $path
 7. iLasm (ILDASM)

# deal with

## main.xxxx.js

 > Why do you modify it here?
 "
 > This is used to explore the use of the console for debugging operations.

 Open the `Fiddler/Resources/APP/OUT/Webserver/ClientApp/Dist/Main.xxx.js`

 Add at the beginning of the function: (please replace the `IE` to the parameter name)

 `` `javascript
 Ie.licenseinfo.CurrenTlicense = "Pro"
 Ie.licenseinfo.hasexpiredtric = false
 Ie.licenseinfo.istrieLalavalect = false
 Ie.licenseinfo.hasValidLicense = TRUE
`` `

 ! [UpdateUserLicense] (pic/main.xxx.js-1.png)

## fiddler.webui.il

 > How do you know to modify this file?
 "
 > When modifying the `main.js` to try to call out the console, the program cannot be started, and the key code is found through the program prompt

 > Modify this file to remove the file verification,
 "
 > At the beginning of version 3.3.0, the verification process was also added. Before that, the modification of this DLL file was optional.
 "
 > After removing the verification of the `TryopeneletronMainMainscript`, you can modify the` app/out/main.js to call out the console

 Do the same operation for the two functions `TryopenClientMainScript` and`TryopeneletronMainscript`:

 Modify the contents of the function body to return directly `true`

 Delete all code before the following code (the following code means `Return True;`)

 `` `
 IL_0208: / * 17 | * / LDC.I4.1
 IL_0209: / * 2A | * / RET
`` `

 !

 This effect is probably after deleting:

 !

## fiddlerbackendsdk.il

 > How do you know to modify this file?
 "
 > This is the data captured by replacing the verification server, and the operation is a bit troublesome;
 "
 > However, if you make a more detailed recovery of the verification server, it should be offline.

### METHOD FIDDLERBACKENDSDK.USER.USERCLIENT :: getbestaccount

 Search `userclient :: getbestaccount`

 Delete IL_000D -IL_0020 corresponding if statement

 Delete IL_003F -IL_0040 corresponding `Return Null;

 ! [Getbestaccount]

### METHOD '<> C__DISPLAYCLASS18_0' :: <<Getbestaccount> B__0 '

 Search `<Getbestaccount> B__0`

 Delete IL_0000 -IL_0019, insert `ldc.i4.1` before IL_001e (that is, the function body returns directly`true`)

 ! [Getbestaccount] (PIC/DLL-Getbestaccount-2.png)
