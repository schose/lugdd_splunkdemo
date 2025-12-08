# tlug-splunk


### start slides
docker run --rm --init -v $PWD/marp:/home/marp/app -e LANG=$LANG -p 8080:8080 -p 37717:37717 marpteam/marp-cli -s .

### run instance

```
aws ec2 run-instances --cli-input-yaml file://demo/singleinstance.yml --user-data file://demo/singleinstance-cloudinit.yml --output yaml
```

###

- get ip
```
aws ec2 describe-instances --filters "Name=instance-state-name,Values=running"  \
--query "Reservations[*].Instances[*].[PublicIpAddress, Tags[?Key=='Name'].Value|[0]]" --output text
```
- connect 
```
ssh -i ~/.ssh/ec2-ffm-2016.pem ec2-user@IP
```

### install 

```
wget -O ~/splunk.tgz https://download.splunk.com/products/splunk/releases/8.2.1/linux/splunk-8.2.1-ddff1c41e5cf-Linux-x86_64.tgz
tar zxfv splunk.tgz
~/splunk/bin/splunk start --accept-license

wget http://docs.splunk.com/images/Tutorial/tutorialdata.zip
unzip tutorialdata.zip
```

~/splunk/bin/splunk add oneshot www1/access.log -sourcetype access_combined -host www1  -auth admin:Password01
~/splunk/bin/splunk add oneshot www2/access.log -sourcetype access_combined -host www2  -auth admin:Password01
~/splunk/bin/splunk add oneshot www3/access.log -sourcetype access_combined -host www3  -auth admin:Password01

~/splunk/bin/splunk add oneshot www1/secure.log -sourcetype linux_secure -host www1  -auth admin:Password01
~/splunk/bin/splunk add oneshot www2/secure.log -sourcetype linux_secure -host www2  -auth admin:Password01
~/splunk/bin/splunk add oneshot www3/secure.log -sourcetype linux_secure -host www3  -auth admin:Password01



### working with splunk

sourcetype=access_combined | stats count
sourcetype=access_combined status=500 | timechart span=1h count by host
sourcetype="access_combined" | stats sum(bytes) as bytes by host | eval MB=round(bytes/1024/1024,1) | table host MB

sourcetype=linux_secure | rex field=_raw "(?<ip>\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3})" | iplocation ip | geostats count by Country

sourcetype=linux_secure eventtype=ssh*  | top eventtype

system/local/inputs.conf

```
[journald]
interval = 10
journalctl-quiet = true
journalctl-include-fields =

[journald://my-stanza]
index = main
```

system/local/fields.conf

```
[sourcetype::journald::*]
INDEXED = true
```

logger --id=1234 -t splunk "please enter credit card number"
