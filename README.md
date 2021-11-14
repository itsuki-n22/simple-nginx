# Nginx Template

This is a template makes it easy to get started with Nginx by using AWS Cloud Formation.

## USAGE
### Start and Activate Server
0. download AWS CLI
1. `cp params.cfg.sample params.cfg`
2. edit params.cfg
3. `aws cloudformation deploy --stack-name <arbitary-stack-name> --template-file template.yml --parameter-overrides $(cat params.cfg)`

### Delete Server
`aws cloudformation delete-stack --stack-name <arbitary-stack-name>`

### About params.cfg

KEYNAME: EC2 key pair name.
AppName: Application name, this can be whatever you like.
AllowedIP: You can restrict SSH access IP. If you don't want to do it, just input '0.0.0.0/32'.
