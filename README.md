AWS CLI commands to import a CSV file into DynamoDB

https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/S3DataImport.HowItWorks.html
https://awscli.amazonaws.com/v2/documentation/api/latest/index.html

install latest CLI version. 2.7.25 required

```
aws --version
```

https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

example:
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64-2.7.25.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install --update
```

create S3 bucket

```
aws s3api create-bucket --bucket my-bucket-random-name-2022-08-19-abcd --region us-east-1
```

send local csv file to S3 bucket

```
aws s3api put-object --bucket my-bucket-random-name-2022-08-19-abcd --key data.csv --body data.csv
```

import data into dynamoDB

```
aws dynamodb import-table --s3-bucket-source S3Bucket=my-bucket-random-name-2022-08-19-abcd --input-format CSV --table-creation-parameters '{"TableName":"target-table","KeySchema":              [{"AttributeName":"hk","KeyType":"HASH"}],"AttributeDefinitions":[{"AttributeName":"hk","AttributeType":"S"}],"BillingMode":"PAY_PER_REQUEST"}'
```


delete object from s3

```
aws s3api delete-object --bucket my-bucket-random-name-2022-08-19-abcd --key data.csv
```

delete S3 bucket

```
aws s3api delete-bucket --bucket my-bucket-random-name-2022-08-19-abcd --region us-east-1
```

delete dynamoDB table

```
aws dynamodb delete-table --table-name target-table
```

