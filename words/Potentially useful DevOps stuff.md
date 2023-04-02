## CLI things
[https://dev.to/lissy93/cli-tools-you-cant-live-without-57f6](https://dev.to/lissy93/cli-tools-you-cant-live-without-57f6)

## Autodetect config issues
[https://github.com/jonrau1/ElectricEye](https://github.com/jonrau1/ElectricEye)

## Kryptoslogic telltale

[https://www.kryptoslogic.com/products/telltale/index.html](https://www.kryptoslogic.com/products/telltale/index.html)

Security host monitoring with a free tier

## Open source

[https://github.com/todogroup](https://github.com/todogroup)

Generic docs for open source docs

## Security
### Not yet tried
[https://github.com/nozaq/terraform-aws-secure-baseline](https://github.com/nozaq/terraform-aws-secure-baseline)
[https://github.com/9rnt/poro](https://github.com/9rnt/poro)
[https://twitter.com/liam_galvin/status/1559471247783870464?t=wTpsoGtxkGjse3SghctQYQ&s=03](https://twitter.com/liam_galvin/status/1559471247783870464?t=wTpsoGtxkGjse3SghctQYQ&s=03) (Trivy for AWS accounts)
[https://github.com/raspbernetes/k8s-security-policies](https://github.com/raspbernetes/k8s-security-policies) # CIS Policies for OPA!
[https://github.com/chaos-mesh/chaos-mesh](https://github.com/chaos-mesh/chaos-mesh)
[https://www.hackread.com/free-best-osint-tools-2021/](https://www.hackread.com/free-best-osint-tools-2021/)
[https://github.com/inguardians/peirates](https://github.com/inguardians/peirates)
[https://github.com/awslabs/assisted-log-enabler-for-aws](https://github.com/awslabs/assisted-log-enabler-for-aws)

[Securing your AWS landscape](https://www.chrisfarris.com/post/aws-ir)

Talk to your company's lawyers before using this, lol

### Tried

[https://github.com/brompwnie/botb](https://github.com/brompwnie/botb)

Tried to break out of some containers in the EKS clusters of VanMoof with this, but not much worked :/ 

[https://github.com/aquasecurity/kube-bench](https://github.com/aquasecurity/kube-bench)

Benchmarking tool for the CIS recommendations matching of a K8s cluster.
Somewhat useful results, but not too impressive

[https://github.com/derailed/popeye](https://github.com/derailed/popeye)

Pretty legit CLI tool (derailed has also made k9s). Findings were decent and actionable, though the RBAC seems to have been subpar somehow because it failed to list all resource types

## DevOps generic

[https://github.com/boz/kail](https://github.com/boz/kail)
[https://github.com/aquasecurity/tfsec](https://github.com/aquasecurity/tfsec)
[https://github.com/falcosecurity/falco](https://github.com/falcosecurity/falco)
[https://github.com/roshan8/slo-tracker](https://github.com/roshan8/slo-tracker)
[https://codeberg.org/hjacobs/kube-downscaler](https://codeberg.org/hjacobs/kube-downscaler)


[https://goteleport.com/kubernetes-access/](https://goteleport.com/kubernetes-access/)  

Reverse SSH tunnel. Talked to them at Kubecon:  [[Vendors I talked to at Kubecon]]
When asked in VanMoof about this my response was:
> The cloud team are aware of Teleport and similar implementations. We do not have a conclusive answer yet, but are leaning towards avoiding SSH as much as possible.
> 
> Longer answer:  
I personally like the design behind the tool, and I spent quite some time talking to their team in Kubecon. I however hope to not need it. This is because SSH workflows by definition serve to mutate a running system and mutating in an IaC world is really not what we should be doing.
> 
P.S If you're talking about SSHing to Nodes (instead of Pods), that's ofc completely out of the question, but I don't think you are

### Pricing and cost

[https://aws.amazon.com/blogs/containers/aws-and-kubecost-collaborate-to-deliver-cost-monitoring-for-eks-customers/](https://aws.amazon.com/blogs/containers/aws-and-kubecost-collaborate-to-deliver-cost-monitoring-for-eks-customers/)
infracost.io

## Internal tooling
airplane.dev

## Policies

[https://www.conftest.dev/](https://www.conftest.dev/)

Tool for policy testing, meant for running in CI
Looks interesting, but would need manual work to write stuff,
or to find good pools of existing tests as a base to extend

## Focus optimizing?
[https://www.centered.app/g/freakin-nerds](https://www.centered.app/g/freakin-nerds)

## Monitoring

[https://github.com/k8spacket/k8spacket](https://github.com/k8spacket/k8spacket)
[https://github.com/netdata/netdata](https://github.com/netdata/netdata)

Pretty cool, ultrafast open source monitoring tool with plenty of builtin integrations

[https://github.com/slok/sloth](https://github.com/slok/sloth)
[https://sloth.dev/usage/cli/](https://sloth.dev/usage/cli/)
[https://sloth.dev/introduction/dashboards/](https://sloth.dev/introduction/dashboards/)

SLO Tracking in Prometheus format. Has Grafana dashboards too

## Green stuff

[https://github.com/thegreenwebfoundation/lighthouse-plugin-greenhouse](https://github.com/thegreenwebfoundation/lighthouse-plugin-greenhouse)

[https://www.thegreenwebfoundation.org/directory/](https://www.thegreenwebfoundation.org/directory/)