Terraform is an [[Infrastructure as Code]] tool that uses Declarative Configuration in HCL (Hashicorp Markup Language)

## Parallelism
I haven't observed parallelism to create a meaningful difference, at least not in my cloudfiles repo which uses a lot of local files. Perhaps it would be different in modules with many more resources?

## Working with non-UTF8 files:

filebase64(...) is your friend

```
resource "local_file" "copy_file_nontext" {  
  content_base64 = filebase64("${path.module}/filename")  
  filename = pathexpand("~/filename_target")  
}
```

#terraform #iac 