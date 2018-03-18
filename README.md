# AWS Clojure Sample Lambda Function

Testing writing lambda functions in clojure, following the [Blop post](https://aws.amazon.com/blogs/compute/clojure/).

## Build

Build uberjar so everything is available for lambda to run.

```
lein uberjar
```

## Deploy

Create function initially, be aware that the namespace changes from dashes to
underscore while compileing clj to java.

```
aws lambda create-function --function-name aws-lambda-clj \
    --handler aws_lambda_clj.core::handler \
    --runtime java8 \
    --memory 512 \
    --timeout 10 \
    --role arn:aws:iam::awsaccountid:role/lambda_exec_role \
    --zip-file fileb://./target/aws-lambda-clj-0.1.0-SNAPSHOT-standalone.jar
```

Update the function code

```
aws lambda update-function-code --function-name aws-lambda-clj \
    --zip-file fileb://./target/aws-lambda-clj-0.1.0-SNAPSHOT-standalone.jar
```

Update function configuration handler for example

```
aws lambda update-function-code --function-name aws-lambda-clj \
    --handler aws_lambda_clj.core::handler
```



