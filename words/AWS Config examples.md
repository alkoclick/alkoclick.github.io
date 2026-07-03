Full [docs here](docs.aws.amazon.com/cli/v1/userguide/cli-configure-files.html#cli-configure-files-where)

I keep forgetting the formatting for these files and I sometimes have to set them up by hand temporarily, so I'm uploading this for some quick self-referencing!

~/.aws/credentials
```
[default]
aws_access_key_id=AKIAIOSFODNN7EXAMPLE
aws_secret_access_key=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY

[user1]
aws_access_key_id=AKIAI44QH8DHBEXAMPLE
aws_secret_access_key=je7MtGbClwBF/2Zp9Utk/h3yCo8nvbEXAMPLEKEY
```

~/.aws/config
```
[default]
region=us-west-2
output=json

[profile user1]
region=us-east-1
output=text
```