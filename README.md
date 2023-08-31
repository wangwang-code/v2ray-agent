自用 即使端口开放检查失败仍然继续 使用非80端口获取证书

做了什么？

注释掉exit 0

```
if [[ "${checkPortOpenResult}" == "fjkvymb6len" ]]; then
        echoContent green " ---> 检测到${port}端口已开放"
    else
        echoContent green " ---> 未检测到${port}端口开放，退出安装"
        if echo "${checkPortOpenResult}" | grep -q "cloudflare"; then
            echoContent yellow " ---> 请关闭云朵后等待三分钟重新尝试"
        else
            echoContent red " ---> 错误日志：${checkPortOpenResult}，如果日志不为空可以提交issue反馈"
        fi
        #exit 0
    fi
```

添加`--httpport`自行修改`NAT端口`为自己小鸡的端口，默认为20348，您可以在"/etc/v2ray-agent/"找到install.sh并修改`1461`行

```
sudo "$HOME/.acme.sh/acme.sh" --issue -d "${tlsDomain}" --standalone --httpport NAT端口 -k ec-256 --server "${sslType}" ${installSSLIPv6} 2>&1 | tee -a /etc/v2ray-agent/tls/acme.log >/dev/null
```
