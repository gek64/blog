# start

```sh
cmd
set http_proxy=http://192.168.1.2:1081
set https_proxy=http://192.168.1.2:1081
set PATH=%PATH%;"%USERPROFILE%\Documents\git\bin"
git config --global http.proxy http://192.168.1.2:1081
git config --global https.proxy http://192.168.1.2:1081 
git config --global --unset http.proxy
git config --global --get http.proxy
```