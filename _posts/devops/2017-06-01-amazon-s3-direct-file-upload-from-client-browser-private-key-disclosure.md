---
layout: post
comments: true
categories: devops
---


## Amazon S3 direct file upload from client browser - private key disclosure
Create an Amazon S3 bucket and configure CORS
CORS needs to be configured on the Amazon S3 bucket to be accessed directly from JavaScript in the browser.
Navigate to the Amazon S3 console.
Choose an existing bucket or create a new bucket if desired. Note the bucket name and bucket region for later use in the application.

Click the Properties tab, open the Permissions section, and click Edit CORS Configuration.

Copy the below XML into the text box and click Save.

----
```
<?xml version="1.0" encoding="UTF-8"?>

<CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01">

   <CORSRule>

      <AllowedOrigin>*</AllowedOrigin>

      <AllowedMethod>GET</AllowedMethod>

      <AllowedMethod>PUT</AllowedMethod>

      <AllowedMethod>POST</AllowedMethod>

      <AllowedMethod>DELETE</AllowedMethod>

      <AllowedHeader>*</AllowedHeader>

   </CORSRule>

</CORSConfiguration>

```


You can upload files on AWS S3 using a server side solution, but in case of larger files it is advisable to use a client side solution. You can probably use JavaScript file upload feature of AWS S3. This is simple three step feature as described below:

Step 1 : In the head section of your page include javascript sdk and specify your keys like this:
	
<script src="https://sdk.amazonaws.com/js/aws-sdk-2.1.24.min.js"></script>
<script type="text/javascript">
    AWS.config.update({
        accessKeyId : 'ACCESS_KEY',
        secretAccessKey : 'SECRET_KEY'
    });
    AWS.config.region = 'AWS_REGION';
</script>

Step 2 : Now create a simple html form with a file input.
	
```
<form id="fileUploadForm" method="post" enctype="multipart/form-data">
<input type="file" name="file" id="file" value="dataFile" required="">
</form>
```

Step 3 : Now upload your input file to S3
	
```
$("#fileUploadForm").submit(function() {
var bucket = new AWS.S3({params: {Bucket: 'BUCKET_NAME'}});
var fileChooser = document.getElementById('file');
var file = fileChooser.files[0];
if (file) {
var params = {Key: 'FILE_NAME', ContentType: file.type, Body: file};
bucket.upload(params).on('httpUploadProgress', function(evt) {
console.log("Uploaded :: " + parseInt((evt.loaded * 100) / evt.total)+'%');
}).send(function(err, data) {
alert("File uploaded successfully.");
});
}
return false;
});
```

To upload the file successfully, you need to enable CORS configuration on S3.
   
Generally, it is not advisable to display your keys directly on page, so you can use Amazon Cognito or web identity federation feature.


Using Cognito service
```
<!DOCTYPE html>
<html>

<head>
    <title>AWS S3 File Upload</title>
    <script src="https://sdk.amazonaws.com/js/aws-sdk-2.1.12.min.js"></script>
</head>

<body>
    <input type="file" id="file-chooser" />
    <button id="upload-button">Upload to S3</button>
    <div id="results"></div>
    <script type="text/javascript">
    AWS.config.region = 'ap-south-1'; // 1. Enter your region

    AWS.config.credentials = new AWS.CognitoIdentityCredentials({
        IdentityPoolId: 'ap-south-1:79a1d229-dd96-4c05-a7de-ef9d58976122' // 2. Enter your identity pool
    });

    AWS.config.credentials.get(function(err) {
        if (err) alert(err);
        console.log(AWS.config.credentials);
    });

    var bucketName = 'test-marcom'; // Enter your bucket name
    var bucket = new AWS.S3({
        params: {
            Bucket: bucketName
        }
    });

    var fileChooser = document.getElementById('file-chooser');
    var button = document.getElementById('upload-button');
    var results = document.getElementById('results');
    button.addEventListener('click', function() {

        var file = fileChooser.files[0];

        if (file) {

            results.innerHTML = '';
            var objKey = 'testing/' + file.name;
            var params = {
                Key: objKey,
                ContentType: file.type,
                Body: file,
                ACL: 'public-read'
            };

            bucket.putObject(params, function(err, data) {
                if (err) {
                    results.innerHTML = 'ERROR: ' + err;
                } else {
                    listObjs();
                }
            });
        } else {
            results.innerHTML = 'Nothing to upload.';
        }
    }, false);
    function listObjs() {
        var prefix = 'testing';
        bucket.listObjects({
            Prefix: prefix
        }, function(err, data) {
            if (err) {
                results.innerHTML = 'ERROR: ' + err;
            } else {
                var objKeys = "";
                data.Contents.forEach(function(obj) {
                    objKeys += obj.Key + "<br>";
                });
                results.innerHTML = objKeys;
            }
        });
    }
    </script>
</body>

</html>
```