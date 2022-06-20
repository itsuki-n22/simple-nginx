# Nginx Template

This is a template makes it easy to get started with Nginx by using AWS Cloud Formation.

## USAGE
### Start and Activate Server
0. download AWS CLI
1. `cp params.cfg.sample params.cfg`
2. `aws ec2 create-key-pair --key-name simple-nginx | jq -r '.KeyMaterial' > simple-nginx.pem`
3. edit params.cfg
4. `aws cloudformation deploy --stack-name simple-nginx --template-file template.yml --parameter-overrides $(cat params.cfg)`
5. wait 10min
6. `aws ec2 describe-instances | jq '.Reservations[].Instances[] | select(.KeyName == "simple-nginx") | .PublicIpAddress'`
7. access `http://x.x.x.x` (where x.x.x.x is IP address got at 6.)

### To Enter EC2

8. `chmod 600 simple-nginx.pem`
9. `ssh -i ./simple-nginx.pem ec2-user@x.x.x.x` (where x.x.x.x is IP address got at 6.)

### Delete Server
`aws cloudformation delete-stack --stack-name simple-nginx`

### Delete KeyPair
`aws ec2 delete-key-pair --key-name simple-nginx`

### About params.cfg

KEYNAME: EC2 key pair name.  
AppName: Application name, this can be whatever you like.  
AllowedIP: You can restrict SSH access IP. If you don't want to do it, just input '0.0.0.0/32'.  
