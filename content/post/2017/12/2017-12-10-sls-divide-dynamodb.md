+++
title = "Serverless FrameworkでDynamoDBのテーブルをstageで分ける"
slug = "sls-divide-dynamodb"
description = ""
date = "2017-12-10T01:29:38+09:00"
categories = []
tags = []
thumbnail = ""
author = "nabeen"
+++

今回は、Serverless FrameworkでDynamoDBをstageによって分ける書き方のメモです。

[nabeen/linebot\-kotlin](https://github.com/nabeen/linebot-kotlin)

## 参考サイト

こちらが参考になりました。

- [Serverless Framework で DynamoDB を使う \- Qiita](https://qiita.com/katsuhiko/items/a2594e73108728a22410)

## 書き方

参考サイトではstageに応じたプレフィックスをつけることで対応していますが、僕は設定ファイルから読み出す方法で書きました。

詳細はGithubを見ていただくとして、ここでは関係している部分のみ抜粋します。

まずは`serverless.yml`の`Resource`の部分、

```yml
provider:
  name: aws
  runtime: java8
#  profile: serverless

# you can overwrite defaults here
  stage: ${opt:stage, self:custom.defaultStage}
  region: ap-northeast-1
# you can add statements to the Lambda function's IAM Role here
  iamRoleStatements:
    - Effect: "Allow"
      Action:
        - dynamodb:GetItem
        - dynamodb:PutItem
        - dynamodb:DescribeStream
        - dynamodb:ListStream
        - dynamodb:GetRecords
        - dynamodb:GetShardIterator
      Resource: 
        - arn:aws:dynamodb:*:*:table/${self:custom.otherfile.environment.${self:provider.stage}.TABLE_NAME}
        - Fn::GetAtt: [LineBotDynamodb, StreamArn]
```

そして同じく`serverless.yml`の`TableName`の部分です。

```yml
resources:
  Resources:
    LineBotDynamodb:
      Type: AWS::DynamoDB::Table
      Properties:
        TableName: ${self:custom.otherfile.environment.${self:provider.stage}.TABLE_NAME}
        AttributeDefinitions:
          - AttributeName: id
            AttributeType: S
        KeySchema:
          - AttributeName: id
            KeyType: HASH
        ProvisionedThroughput:
          ReadCapacityUnits: 1
          WriteCapacityUnits: 1
        StreamSpecification:
          StreamViewType: NEW_IMAGE
```

これでOK。

`TABLE_NAME`はプログラム側でも使う数値なので、環境変数に設定するのもお忘れなく。
