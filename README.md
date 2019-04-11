# helpful-aws-scripts
some helpful aws scripts



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


AWS.config.loadFromPath('./credentials_david.json')

//const sts = new AWS.STS({apiVersion: '2011-06-15'})
const sts = new AWS.STS()


  const quicksighta = new AWS.Service(quicksightParams)
    /*quicksighta.listUsers({
      'AwsAccountId': '000000000000',
      'Namespace': 'default'
    }, function(data, err) {
      console.log(data)
      console.log(err)
    })*/
/*
quicksight.getDashboardEmbedUrl({
      'AwsAccountId': '000000000000',
      'DashboardId': '1234567-1234-1234-1234-123456789012',
      'IdentityType': 'IAM',
      'ResetDisabled': true,
      'SessionLifetimeInMinutes': 100,
      'UndoRedoDisabled': false
  }, function(err, data) {
    if (err) console.log(err, err.stack); // an error occurred
    else     console.log(data.EmbedUrl);           // successful response
  })



  */
function start(){

sts.assumeRole({
  DurationSeconds: 3600,
  RoleArn: 'arn:aws:iam::0123456789012:role/Quicksight-dashboard-embedded',
  // ExternalId: '1234567-1234-1234-1234-123456789012',
  //RoleSessionName: 'embeddingsessiona'
  RoleSessionName: 'embeddingDashboardSession_Carmel'

}, function(err, newSession) {
  if (err) { // an error occurred
    console.log('Cannot assume role');
    console.log(err, err.stack);
  } else { // successful response
    //console.log(newSession)
    //AWS.config.credentials = new AWS.EnvironmentCredentials('AWS');

// Now set temporary credentials seeded from the master credentials
      /*
    AWS.config.update({
      // region: 'localhost',
      region: 'us-east-1',
          accessKeyId: newSession.Credentials.AccessKeyId,
          secretAccessKey: newSession.Credentials.SecretAccessKey,
          sessionToken: newSession.Credentials.SessionToken
    })
    */
    //AWS.config.credentials = new AWS.EnvironmentCredentials('AWS');
      /*AWS.config.credentials = new AWS.TemporaryCredentials({
  RoleArn: 'arn:aws:sts::0123456789012:assumed-role/Quicksight-dashboard-embedded',
  // RoleSessionName: 'embeddingDashboardSession_Carmela'
});*/
    //AWS.config.credentials = new AWS.EnvironmentCredentials('AWS');
      /*AWS.config.credentials = new AWS.TemporaryCredentials({
  RoleArn: 'arn:aws:sts::863657571044:assumed-role/Quicksight-dashboard-embedded',
  // RoleSessionName: 'embeddingDashboardSession_Carmela'
});*/



  AWS.config.credentials = new AWS.Credentials({
      accessKeyId: newSession.Credentials.AccessKeyId,
      secretAccessKey: newSession.Credentials.SecretAccessKey,
      sessionToken: newSession.Credentials.SessionToken
  })

  const quicksight = new AWS.Service(quicksightParams)
    AWS.config.region = "us-east-1";


	  /*process.env.AWS_ACCESS_KEY_ID=newSession.Credentials.AccessKeyId
	  process.env.AWS_SECRET_ACCESS_KEY=newSession.Credentials.SecretAccessKey
	  process.env.AWS_SESSION_TOKEN=newSession.Credentials.SessionToken*/
/*process.env.AWS_ACCESS_KEY_ID = newSession.Credentials.AccessKeyId;
  process.env.AWS_SECRET_ACCESS_KEY = newSession.Credentials.SecretAccessKey;
  process.env.AWS_SESSION_TOKEN = newSession.Credentials.SessionToken;
  process.env.AWS_SECURITY_TOKEN = newSession.Credentials.SessionToken;
    AWS.config.credentials.refresh( (a, b) => {
console.log(a)
console.log(b)
    } )
    */
  /*const sts1 = new AWS.STS()
  sts1.getCallerIdentity({}, function(err, data) {
    if (err) console.log(err, err.stack); // an error occurred
    else
      console.log(data);           // successful response
  })*/

    // console.log(process.env.AWS_ACCESS_KEY_ID)

    /* console.log(`export AWS_ACCESS_KEY_ID=${newSession.Credentials.AccessKeyId}`)
	  console.log(`export AWS_SECRET_ACCESS_KEY=${newSession.Credentials.SecretAccessKey}`)
    console.log(`export AWS_SESSION_TOKEN=${newSession.Credentials.SessionToken}`)*/

	// console.log(newSession.Credentials)
	//console.log(AWS.config)
	//console.log(newSession)
	//console.log(AWS.config.credentials)

  var params = {

  };
    //    console.log("==============================================================================================================================")

  quicksight.getDashboardEmbedUrl({
      'AwsAccountId': '0123456789012',
      'DashboardId': '',
      'IdentityType': 'IAM',
      'ResetDisabled': true,
      'SessionLifetimeInMinutes': 100,
      'UndoRedoDisabled': false
  }, function(err, data) {
    if (err) console.log(err, err.stack); // an error occurred
    else     console.log(data.EmbedUrl);           // successful response
  })

/*
  sts.getCallerIdentity(params, function(err, data) {
          if (err) console.log(err, err.stack); // an error occurred
    else
      console.log(data);           // successful response
  })
*/

    /*
  quicksight.getDashboardEmbedUrl({
      'AwsAccountId': '0123456789012',
      'DashboardId': '000000-0000-0000-0000-000000000',
      'IdentityType': 'IAM',
      'ResetDisabled': true,
      'SessionLifetimeInMinutes': 100,
      'UndoRedoDisabled': false
  }, function(err, data) {
    if (err) console.log(err, err.stack); // an error occurred
    else     console.log(data.EmbedUrl);           // successful response
  })
      */


  }
})


}


/*quicksight.getDashboardEmbedUrl({
    'AwsAccountId': '0123456789012',
    'DashboardId': '000000-0000-0000-0000-000000000',
    'IdentityType': 'IAM',
    'ResetDisabled': true,
    'SessionLifetimeInMinutes': 100,
    'UndoRedoDisabled': false
}, function(err, data) {
  if (err) console.log(err, err.stack); // an error occurred
  else     console.log(data);           // successful response
})*/

start()


```
