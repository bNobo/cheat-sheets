# SSL / TLS

## Fix missing local certificate in curl (bash GIT)

Add the missing certificates to `C:\Program Files\Git\mingw64\ssl\certs\ca-bundle.crt`. For exemple, Sectigo intermediate certificates can be obtained from [here](https://sectigostore.com/page/sectigo-ca-bundle/)

## Workaround missing local certificate in Insomnia

Add the missing certificates to `C:\Users\rocco\AppData\Local\Temp\insomnia_2021.6.0\ca-certs.pem`. Renew the operation with each update.

There is an open pull request that load certificates from Windows Store : https://github.com/Kong/insomnia/pull/3203
