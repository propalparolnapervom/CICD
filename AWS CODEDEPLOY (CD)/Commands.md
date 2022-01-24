## Docs

[Create Deployment via CLI](https://docs.aws.amazon.com/codedeploy/latest/userguide/deployments-create-cli.html)

 
## List

List `Applications`, registered with the IAM user or AWS account.
```
aws deploy list-applications

  # OR
  
aws deploy list-applications \
--region ap-southeast-2
```

List `Deployment Groups` for the specific `Application`
```
aws deploy list-deployment-groups \
--application-name burt-testing-app-on-prod

   # OR
   
aws deploy list-deployment-groups \
--application-name burt-testing-app-on-prod \
--region ap-southeast-2  
```

Get info about specific `Deployment`
```
aws deploy get-deployment \
--deployment-id d-8XOJO4RJE

   # OR
   
aws deploy get-deployment \
--deployment-id d-8XOJO4RJE \
--region ap-southeast-2  
```


## Deploy

Deploy specific `Deployment`
```
aws deploy create-deployment \
--application-name burt-testing-app-on-prod \
--deployment-group-name burt-testing-deploygroup-on-prod \
--description "Test dummy deployment, manually started by Burtovyi via AWS CLI" \
--region ap-southeast-2 \
--s3-location bucket=to-del-anytime-sydney,key=73629697-73465861-72483598-52a531f4-d6ba-446d-8b81-422f5add451a.zip,bundleType=zip
```


