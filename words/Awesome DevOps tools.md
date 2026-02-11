## Generic

* [https://github.com/boz/kail](https://github.com/boz/kail)
* [https://github.com/aquasecurity/tfsec](https://github.com/aquasecurity/tfsec)
* [https://github.com/falcosecurity/falco](https://github.com/falcosecurity/falco)
* [https://github.com/roshan8/slo-tracker](https://github.com/roshan8/slo-tracker)
* [https://codeberg.org/hjacobs/kube-downscaler](https://codeberg.org/hjacobs/kube-downscaler)
* aws-nuke
* https://github.com/wagoodman/dive
* [https://prometheus.io/webtools/alerting/routing-tree-editor/](https://prometheus.io/webtools/alerting/routing-tree-editor/)
* https://github.com/stan-smith/FossFLOW
Visualisation and isometric diagrams for infra


[https://goteleport.com/kubernetes-access/](https://goteleport.com/kubernetes-access/)  

Reverse SSH tunnel. Talked to them at Kubecon:  [[Vendors I talked to at Kubecon]]
When asked in VanMoof about this my response was:
> The cloud team are aware of Teleport and similar implementations. We do not have a conclusive answer yet, but are leaning towards avoiding SSH as much as possible.
> 
> Longer answer:  
I personally like the design behind the tool, and I spent quite some time talking to their team in Kubecon. I however hope to not need it. This is because SSH workflows by definition serve to mutate a running system and mutating in an IaC world is really not what we should be doing.
> 
P.S If you're talking about SSHing to Nodes (instead of Pods), that's ofc completely out of the question, but I don't think you are


## Visualization
https://github.com/AykutSarac/jsoncrack.com
Visualisation and conversions for JSON stuff

### Pricing and cost
* [https://aws.amazon.com/blogs/containers/aws-and-kubecost-collaborate-to-deliver-cost-monitoring-for-eks-customers/](https://aws.amazon.com/blogs/containers/aws-and-kubecost-collaborate-to-deliver-cost-monitoring-for-eks-customers/)
* infracost.io
* Goldilocks

## Internal tooling
airplane.dev

## Policies

[https://www.conftest.dev/](https://www.conftest.dev/)

Tool for policy testing, meant for running in CI
Looks interesting, but would need manual work to write stuff,
or to find good pools of existing tests as a base to extend

## Controls and auditing
Autodetect config issues
* [https://github.com/jonrau1/ElectricEye](https://github.com/jonrau1/ElectricEye)


## Monitoring
* [https://github.com/k8spacket/k8spacket](https://github.com/k8spacket/k8spacket)
* [https://github.com/netdata/netdata](https://github.com/netdata/netdata)

Pretty cool, ultrafast open source monitoring tool with plenty of builtin integrations

* [https://github.com/slok/sloth](https://github.com/slok/sloth)
* [https://sloth.dev/usage/cli/](https://sloth.dev/usage/cli/)
* [https://sloth.dev/introduction/dashboards/](https://sloth.dev/introduction/dashboards/)

SLO Tracking in Prometheus format. Has Grafana dashboards too. I've heard heavy criticisms of how many recording rules it generates tho

## FaaS
* [https://www.val.town/](https://www.val.town/)
