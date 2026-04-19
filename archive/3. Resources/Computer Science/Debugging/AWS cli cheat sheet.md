```Shell
aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 464544971725.dkr.ecr.ap-south-1.amazonaws.com
```


```Shell
aws ssm start-session --target  i-0b0052a1f8fc6629c
```


```
aws cloudformation create-stack --stack-name bms-prod-apm-cft --template-body file://///Users/viraj.bharvada/SRE/cloudformation/bms-prod-cft-v1/bms-cfn-infrafiles/bms-prod-apm-cft/apmlogs-db-resources-v-1.6.yml --parameters file:////Users/viraj.bharvada/SRE/cloudformation/bms-prod-cft-v1/bms-cfn-infrafiles/bms-prod-apm-cft/apmlogs-prod-parameters-v-1.6.json --region ap-south-1 --profile aws-prod
```