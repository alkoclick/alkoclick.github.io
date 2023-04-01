```terraform
data "external" "no_default_workspace" {
  # This little program will blow up at plan time if you try to run a plan in the default workspace
  # We include it in repositories where you should never do stuff at the default workspace
  # Please switch to the workspace "production" or otherwise check what's available with `terraform workspace list`
  program = ["sh", "-c", "[ $(terraform workspace show) != \"default\" ] && echo {}"]
}
```