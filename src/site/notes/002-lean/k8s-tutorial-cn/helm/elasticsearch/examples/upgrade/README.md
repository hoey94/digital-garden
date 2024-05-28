---
{"dg-publish":true,"permalink":"/002-lean/k8s-tutorial-cn/helm/elasticsearch/examples/upgrade/README/","dgPassFrontmatter":true}
---


# Upgrade

This example will deploy a 3 node Elasticsearch cluster chart using an old chart
version, then upgrade it.


## Usage

* Deploy and upgrade Elasticsearch chart with the default values: `make install`


## Testing

You can also run [goss integration tests][] using `make test`.


[goss integration tests]: https://github.com/elastic/helm-charts/tree/main/elasticsearch/examples/upgrade/test/goss.yaml