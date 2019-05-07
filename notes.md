#Install
```
time ansible-playbook  -i ~/ansible/non-prod-hosts -u eodell --key-file ~/.ssh/id_rsa-ucop -b -e "cli_key=$key" -e "cli_secret=$secret" -f 15  aws-cloudwatch.yaml
```

#Insights

```
fields @timestamp, @message
| filter (@message like /(?i)error/ or like /(?i)fail/)
| stats count(*) as nope by @logStream
| sort nope desc
| limit 2000
```
```
fields @timestamp, @message
| stats count(*) as streams by @logStream
| filter @logStream like /message/
| sort streams desc
| limit 2000
```
```
fields @timestamp, @message
| sort @timestamp desc
| filter (@message like /(?i)error/ or @message like /(?i)fail/)
| stats count(*) as streams by @logStream
| sort streams desc
| limit 20000
```
