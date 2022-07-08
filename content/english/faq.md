---
title: "FAQ"
heading: "Having a question?"
draft: false
_build:
  render: never

image: "images/feature-image-3.webp"

faq:
- title: "How secure is my data in EasyServices?"
  content: "Our datacenters of our hosting provider (Hetzner) are heavily guarded and all communication happens SSL encrypted, unless your service is using something else on purpose. Hetzner is one of the biggest providers in Europe, and is historically reliable."
- title: "What encryption do you use?"
  content: "Traffic is SSL encrypted, using the newest TLS 1.3 protocol, and isolated using custom subnets of Kubernetes."
- title: "What is your SLA? How much downtime do I have to expect?"
  content: "If you are using multi-zone services the network SLA is 99.9%. If one datacenters fails services are automatically transacted to the second datacenter in seconds, therefore avoiding downtime."
- title: "What happens if I need help?"
  content: "If the problem is caused on our end help is free, but unless bigger cloud providers we are offering consultation and developer hours as well. You do not have to worry about anything, and we can fully support you in your cloud transformation."
---