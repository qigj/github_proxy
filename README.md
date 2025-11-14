# Github Proxy

#### Github 加速代理

#### 使用方法
```
# 例如第一个域名 1.github.010716.xyz

https://1.github.010716.xyz/https://raw.githubusercontent.com/qigj/github_proxy/refs/heads/main/Textfile
```

#### 自动检测脚本
wget
```bash
wget --timeout=5 --tries=1 -qO- https://gitee.com/qigj/github_proxy/raw/master/github_proxy_list.txt|while read GITHUB_PROXY;do wget --timeout=5 --tries=1 -qO- "https://${GITHUB_PROXY}/https://raw.githubusercontent.com/qigj/github_proxy/refs/heads/main/Textfile" 2>/dev/null|grep -q 917faa3e-3faf-4f4e-8f45-ac3d1eb43856 && echo "Github代理地址: https://$GITHUB_PROXY/" && break;done
```
curl
```bash
curl -s --max-time 5 https://gitee.com/qigj/github_proxy/raw/master/github_proxy_list.txt|while read GITHUB_PROXY;do curl -s --max-time 5 "https://${GITHUB_PROXY}/https://raw.githubusercontent.com/qigj/github_proxy/refs/heads/main/Textfile" 2>/dev/null|grep -q 917faa3e-3faf-4f4e-8f45-ac3d1eb43856 && echo "Github代理地址: https://$GITHUB_PROXY/" && break;done
```
#### 直接单独当作函数调用
``` bash
curl_github_proxy() {
    log "🔍 检查 Github Proxy ..."
    curl -s --max-time 5 https://gitee.com/qigj/github_proxy/raw/master/github_proxy_list.txt | while read GITHUB_PROXY; do \
    curl -s --max-time 5 "https://${GITHUB_PROXY}/https://raw.githubusercontent.com/qigj/github_proxy/refs/heads/main/Textfile" 2>/dev/null|grep -q 917faa3e-3faf-4f4e-8f45-ac3d1eb43856 && log "✅ Github代理地址: https://$GITHUB_PROXY/" &&  \
    curl https://$GITHUB_PROXY/$@ && break; done
}
curl_github_proxy "$DOWNLOAD_URL" -sL --max-time 180 -o "$INSTALL_DIR/$TAR_NAME" || { log "❌ 下载失败"; return; }

```
