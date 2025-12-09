# tlug-splunk


### start slides

```bash
docker run --rm --init -v $PWD/marp:/home/marp/app -e LANG=$LANG -p 8080:8080 -p 37717:37717 marpteam/marp-cli -s .

### run instance

```bash
aws ec2 run-instances --cli-input-yaml file://demo/singleinstance.yml --user-data file://demo/singleinstance-cloudinit.yml --output yaml
```

###

- get ip

```bash
aws ec2 describe-instances --filters "Name=instance-state-name,Values=running"  \
--query "Reservations[*].Instances[*].[PublicIpAddress, Tags[?Key=='Name'].Value|[0]]" --output text
```
- connect

```bash
ssh -i ~/.ssh/ec2-ffm-2016.pem ec2-user@IP
```

### install 

```bash
wget -O ~/splunk.tgz https://download.splunk.com/products/splunk/releases/10.0.2/linux/splunk-10.0.2-e2d18b4767e9-linux-amd64.tgz
tar zxfv splunk.tgz
~/splunk/bin/splunk start --accept-license

wget https://iksdplinux.s3.amazonaws.com/tutorialdata.zip
unzip tutorialdata.zip
```

```bash
~/splunk/bin/splunk add oneshot www1/access.log -sourcetype access_combined -host www1  -auth admin:Password01
~/splunk/bin/splunk add oneshot www2/access.log -sourcetype access_combined -host www2  -auth admin:Password01
~/splunk/bin/splunk add oneshot www3/access.log -sourcetype access_combined -host www3  -auth admin:Password01

~/splunk/bin/splunk add oneshot www1/secure.log -sourcetype linux_secure -host www1  -auth admin:Password01
~/splunk/bin/splunk add oneshot www2/secure.log -sourcetype linux_secure -host www2  -auth admin:Password01
~/splunk/bin/splunk add oneshot www3/secure.log -sourcetype linux_secure -host www3  -auth admin:Password01
```

### working with splunk

```bash
sourcetype=access_combined | stats count
sourcetype=access_combined status=500 | timechart span=1h count by host
sourcetype="access_combined" | stats sum(bytes) as bytes by host | eval MB=round(bytes/1024/1024,1) | table host MB

sourcetype=linux_secure failed password | rex field=_raw "(?<ip>\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3})" | iplocation ip | geostats count by Country

```

system/local/inputs.conf

```
[journald]
interval = 10
journalctl-quiet = true
journalctl-include-fields =

[journald://my-stanza]
index = main
```

logger --id=1234 -t splunk "please enter credit card number"
