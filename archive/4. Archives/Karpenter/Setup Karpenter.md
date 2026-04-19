
```Shell
for NODEGROUP in $(aws eks list-nodegroups --profile aws-tool --cluster-name ${CLUSTER_NAME} \
    --query 'nodegroups' --output text); do aws ec2 create-tags \
        --profile aws-tool --tags "Key=karpenter.sh/discovery,Value=${CLUSTER_NAME}" \
        --resources $(aws eks describe-nodegroup --profile aws-tool --cluster-name ${CLUSTER_NAME} \
        --nodegroup-name $NODEGROUP --query 'nodegroup.subnets' --output text )
done

```


```bash
AWS_ACCOUNT_ID=$(aws sts get-caller-identity --profile aws-tool --query 'Account' \
    --output text)
```

```bash
OIDC_ENDPOINT="$(aws eks describe-cluster --profile default --name ${CLUSTER_NAME} \
    --query "cluster.identity.oidc.issuer" --output text)"
```
```bash
AWS_ACCOUNT_ID=$(aws sts get-caller-identity --profile default --query 'Account' \
    --output text)
```