# PUT
This works for node 18.x  
Why **PutCommand** from @aws-sdk/lib-dynamodb is used instead of **PutItemCommand** from @aws-sdk/client-dynamodb ?  
[stackoverflow](https://stackoverflow.com/questions/57804745/difference-between-aws-sdk-dynamodb-client-and-documentclient)  
Inshort it is easier to use PutCommand(Check the items in params)  

## PutCommand
```js

import { DynamoDBClient } from "@aws-sdk/client-dynamodb";
import { DynamoDBDocumentClient, PutCommand } from "@aws-sdk/lib-dynamodb";

export const handler = async(event) => {
    
    const REGION = "ap-south-1"; 
    const ddbClient = new DynamoDBClient({ region: REGION });
    const ddbDocClient = DynamoDBDocumentClient.from(ddbClient);

        const params = {
        "TableName":"products-table",
        "Item": {
                    category: "laptop" ,
                    productId: "777",
                    usedBy: "Thalaivaaa",
                }
        }
    let data
    try{
        data = await await ddbDocClient.send(new PutCommand(params))
    }
    catch(err){
        console.log(err)
        return{
        statusCode: 500,
        body: JSON.stringify(err),
    };
    }
    return {
        statusCode: 200,
        body: JSON.stringify(data),
    };
};

```

## PutItemCommand
```js

import { DynamoDBClient, PutItemCommand } from "@aws-sdk/client-dynamodb";

export const handler = async(event) => {
    
    const REGION = "ap-south-1"; 
    const ddbClient = new DynamoDBClient({ region: REGION });
    const params = {
        "TableName":"products-table",
        "Item": {
                    category: { S: "laptop" },
                    productId: { S: "564" },
                    usedBy: { S: "Praveen" },
                }
    }
    let data
    try{
        data = await ddbClient.send(new PutItemCommand(params));
    }
    catch(err){
        console.log(err)
        return{
        statusCode: 500,
        body: JSON.stringify(err),
    };
    }
    return {
        statusCode: 200,
        body: JSON.stringify(data),
    };
}

```
