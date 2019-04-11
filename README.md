# helpful-aws-scripts
some helpful aws scripts


## AWS Quicksight get dashboard
```JS

const AWS = require('aws-sdk');
const https = require('https');
const fs = require('fs')
AWS.config.region = 'us-east-1'

const quicksightParams = {
  AwsAccountId: '000000000000',
  DashboardId: '000000-0000-0000-0000-000000000',
	IdentityType: 'IAM',
	apiConfig: require('./quicksight-2018-04-01.min.json'),
}

// optional
AWS.config.loadFromPath('./credentials.json')


sts.assumeRole({
  DurationSeconds: 3600,
  RoleArn: 'arn:aws:iam::0123456789012:role/Quicksight-dashboard-embedded',
  // ExternalId: '1234567-1234-1234-1234-123456789012',
  RoleSessionName: 'embeddingsession'

}, function(err, newSession) {
  if (err) {
    console.log('Cannot assume role');
    console.log(err, err.stack);
  } else {

	// Now set temporary credentials seeded from the master credentials
	  AWS.config.credentials = new AWS.Credentials({
	      accessKeyId: newSession.Credentials.AccessKeyId,
	      secretAccessKey: newSession.Credentials.SecretAccessKey,
	      sessionToken: newSession.Credentials.SessionToken
	  })

	  const quicksight = new AWS.Service(quicksightParams)
	  AWS.config.region = "us-east-1";


	  const newSts = new AWS.STS()
	  newSts.getCallerIdentity({}, function(err, data) {
	    if (err) console.log(err, err.stack);
	    else
	      console.log(data);
	  })

	  quicksight.getDashboardEmbedUrl({
	      'AwsAccountId': '0123456789012',
	      'DashboardId': '',
	      'IdentityType': 'IAM',
	      'ResetDisabled': true,
	      'SessionLifetimeInMinutes': 100,
	      'UndoRedoDisabled': false
	  }, function(err, data) {
	    if (err) console.log(err, err.stack);
	    else     console.log(data.EmbedUrl);
	  })
  }
})

```
