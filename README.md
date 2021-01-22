# Hive.factorio

Setting up factorio to run on Kubernetes cluster. Uses the factorio-docker from factoriotools, but adjusts some shell scripts to work on kubernetes.

Read data path in the container: /opt/factorio/data

Write data path mounted on a persistent volume: /factorio

Binaries path fixed in the container: /opt/factorio/bin


## Original Author

* [factoriotools](https://github.com/factoriotools/factorio-docker) - Original Author
