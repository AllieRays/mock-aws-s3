# Mock AWS S3 SDK

This is a very simple interface that mocks the AWS SDK for Node.js.
It is incomplete as it will mainly be used to test the grunt plugin `grunt-aws-s3`.

Available:
- listObjects
- deleteObjects
- deleteObject
- getObject
- headObject
- putObject
- copyObject
- upload

It uses a directory to mock a bucket and its content.

If you'd like to see some more features or you have some suggestions, feel free to use the issues or submit a pull request.

## Release History
* 2015-11-04   v2.0.0   Static basePath configuration, bound params (by @CJNE) and match upload API (by @kyleseely)
* 2015-10-25   v1.1.0   Removed because of potential breaking change with bound params
* 2015-09-24   v1.0.0   Breaking changes and awesome PR to fix API inconsistencies by @irothschild
* 2015-08-27   v0.5.0   Refactor and default options by @whitingj
* 2015-07-28   v0.4.0   Add headObject method by @mdlavin
* 2015-07-21   v0.3.0   Add CommonPrefixes to listObjects by @jakepruitt
* 2015-03-15   v0.2.7   Mock out AWS' config submodule by @necaris
* 2015-03-13   v0.2.6   Partial match support and ContentLength by @mick
* 2015-03-03   v0.2.5   Allow string and fix tests by @lbud
* 2015-02-05   v0.2.4   Fix url encoding for copy by @ahageali
* 2015-01-22   v0.2.3   Support for copyObject
* 2014-02-02   v0.2.1   Support for deleteObject
* 2014-01-08   v0.2.0   Support streams for getObject/putObject
* 2013-10-24   v0.1.2   Fix isTruncated typo
* 2013-10-09   v0.1.1   Add LastModified to listObject
* 2013-08-09   v0.1.0   First release

## Example

```js
var AWSMock = require('mock-aws-s3');
AWSMock.config.basePath = '/tmp/buckets/' // Can configure a basePath for your local buckets
var s3 = AWSMock.S3({
	params: { Bucket: 'example' }
});
s3.putObject({Key: 'sea/animal.json', Body: '{"is dog":false,"name":"otter","stringified object?":true}'}, function(err, data) {
	s3.listObjects({Prefix: 'sea'}, function (err, data) {
		console.log(data);
	});
});
```
