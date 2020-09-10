# EKS pod 로그 CloudWatch에 저장하기

## 참고링크

- https://docs.aws.amazon.com/ko_kr/AmazonCloudWatch/latest/monitoring/Container-Insights-setup-logs.html

## 주의사항

1. EC2 role -> IRSA 적용

IRAS 추가 + `eks.amazonaws.com/role-arn` annotations 추가

```
apiVersion: v1
kind: ServiceAccount
metadata:
  name: fluentd
  namespace: amazon-cloudwatch
  annotations:
    eks.amazonaws.com/role-arn: xxx
```

AWS_REGION 추가

```
- name: AWS_REGION
  valueFrom:
    configMapKeyRef:
      name: cluster-info
      key: logs.region
```

2. 원하는 로그만 수집

fluent.conf 수정
