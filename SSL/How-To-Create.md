# What we want to do:

we want to:

1. create a private and public key.
2. generate a `cer` file.
3. generate `pfx` file.
4. import `pfx` file in `IIS`.
5. set `https`.



***

# Create a private and public key

go to site `https://csrgenerator.com/` and fill fields as required. then click on generate and copy the entire base64 string generated. save `-----BEGIN CERTIFICATE REQUEST-----` part to a text file named what-ever you want, for example `request.txt`, and `-----BEGIN PRIVATE KEY-----`    to file named what-ever you want, for example `pr.key`.



# Generate `cer` file

go to a `cer` generator and use content of file `requst.txt` to generate a base64 `cer` file. download and save it somewhere in you local machine. for example `c:\ssl\certnew.cer`



**Cation:** it is possible to create it with `openssl`.



***

#  Generate `pfx` file

if you have git installed, it is very likely that `openssl ` is installed and located in path `C:\'Program Files'\Git\usr\bin\`, if not you need to download and install it from `https://slproweb.com/products/Win32OpenSSL.html`.

now execute following command:

```powershell
C:\'Program Files'\Git\usr\bin\openssl.exe pkcs12 -export -in c:\ssl\certnew.cer -inkey c:\ssl\pr.key -out c:\ssl\certnew.pfx
```



this command will ask you to specify a password, enter what ever you desire; a file named `certnew.pfx` will be generated for you.



***

# Import `pfx` in IIS

to do so open IIS and double click on `Server Certificates`, then click on `Import` and specify the path of file `certnew.pfx`, enter the password of your certificate. a record will be added to your `Server Certificates` list.



***

# Set HTTPS

now navigate to your site, click on bindings, click on `Add` button, in the pop up window select `https` as `Type` and select your imported `Server Certificates` as your `SSL certificate` and finally click on `Ok` button.



 