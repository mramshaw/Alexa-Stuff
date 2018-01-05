# DynamoDB

[This information is correct as of January 5, 2018 but things change rapidly in the cloud and documentation becomes out-of-date extremely quickly.]

To persist state across sessions, a database is necessary.

DynamoDB is not expensive, but it's not free either.

On the other hand, DynamoDB integration with node.js is painless.

## Integration with node.js

```node
exports.handler = function (event, context, callback) {
    const alexa = Alexa.handler(event, context, callback);
    alexa.appId = appId;
    alexa.dynamoDBTableName = 'YourTableName';
    alexa.registerHandlers( ... );
    alexa.execute();
};
```

That one line of code is all that's needed!

## Permissions

Best to allocate 'YourTableName' manually rather than give Create permission.

[The table key must be named `userId`.]

Restrict access as follows:

	{
	  "Version": "2012-10-17",
	  "Statement": [
	    {
	      "Effect": "Allow",
	      "Action": [
	        "dynamodb:PutItem",
	        "dynamodb:GetItem"
	      ],
	      "Resource":["arn:aws:dynamodb:us-east-1:xxxxxxxxxxxx:table/YourTableName"],
	    }
	  ]
	}

## Werner Vogels' blog, "All Things Distributed"

The release announcement:

    http://www.allthingsdistributed.com/2012/01/amazon-dynamodb.html

The White Paper (included here):

    http://www.allthingsdistributed.com/files/amazon-dynamo-sosp2007.pdf

## Other links

For more on Werner Vogels:

    http://www.se-radio.net/2006/12/episode-40-interview-werner-vogels/

## To Do

- [ ] Investigate DynamoDB Alerts
- [ ] Investigate Auto-Scaling
