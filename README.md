# 

#### Github 加速代理

#### 使用方法
```
# 例如第一个域名 1.github.010716.xyz

https://1.github.010716.xyz/https://raw.githubusercontent.com/qigj/go_aliddns/refs/heads/master/README.md
```

#### 自动检测脚本
```bash
test_url="https://raw.githubusercontent.com/qigj/go_aliddns/refs/heads/master/README.md"

for proxy in $(wget --timeout=5 --tries=1 -qO- https://gitee.com/qigj/mf/raw/master/github_proxy_list.txt); do
  wget --timeout=5 --tries=1 -qO- "https://${proxy}/${test_url}" 2>/dev/null|grep -q aliyunddns && echo "https://$proxy/" && break
done
```# github_proxy