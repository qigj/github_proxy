# Github_Proxy

#### Github 加速代理

#### 使用方法
```
# 例如第一个域名 1.github.010716.xyz

https://1.github.010716.xyz/https://raw.githubusercontent.com/qigj/github_proxy/refs/heads/main/Textfile
```

#### 自动检测脚本
wget
```bash
test_url="https://raw.githubusercontent.com/qigj/github_proxy/refs/heads/main/Textfile"

for proxy in $(wget --timeout=5 --tries=1 -qO- https://gitee.com/qigj/github_proxy/raw/master/github_proxy_list.txt); do
  wget --timeout=5 --tries=1 -qO- "https://${proxy}/${test_url}" 2>/dev/null|grep -q 917faa3e-3faf-4f4e-8f45-ac3d1eb43856 && echo "https://$proxy/" && break
done
```
curl
```bash
    log "🔍 检查 Github Proxy ..."
    test_url="https://raw.githubusercontent.com/qigj/github_proxy/refs/heads/main/Textfile"

    for GITHUB_PROXY in $(curl -s --max-time 5 https://gitee.com/qigj/github_proxy/raw/master/github_proxy_list.txt); do
        curl -s --max-time 5 "https://${GITHUB_PROXY}/${test_url}" 2>/dev/null|grep -q 917faa3e-3faf-4f4e-8f45-ac3d1eb43856 && log "✅ Github代理地址: https://$GITHUB_PROXY/" &&  \
        break
    done
}
```
