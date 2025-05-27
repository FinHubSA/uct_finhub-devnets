<div align="center"><img src="https://github.com/user-attachments/assets/82038d72-2668-423f-9814-606533a0f5e6" width="100"/></div>

<h1 align="center">How to join the UCT Finhub Devnet</h1>

This guide will demonstrate how to setup nodes on the UCT Finhub testnet (uct_finhub-devnet-1). If the network changes a new network will be added e.g. devnet-2, but the overall setup should remain the same.

# Preparation

The preparation steps are the same as the ones in the guide for [creating an ethereum devnet setup](https://github.com/FinHubSA/ethereum-devnet-setup/tree/main?tab=readme-ov-file#infrastructure-code-for-public-devtestnets-setup).

1. Complete the [setup a gke cluster](https://github.com/FinHubSA/ethereum-devnet-setup/tree/main?tab=readme-ov-file#setup-a-gke-cluster) section
2. Complete the [Setup Kubernetes Commandline Tool (Kubectl)](https://github.com/FinHubSA/ethereum-devnet-setup/tree/main?tab=readme-ov-file#setup-kubernetes-commandline-tool-kubectl) section
3. Complete the [Setup Kurtosis](https://github.com/FinHubSA/ethereum-devnet-setup/tree/main?tab=readme-ov-file#setup-kurtosis) section

# Deploy a participating node 

1. To deploy a node that syncs to an existing network we will use the network config file in this repo, `kurtosis_network_params.yaml` file
    - `network:` -  This parameter will specify the dev network the nodes sync to.
      - The `devnet-1` in the network name is a key word that lets the [ethereum-package](https://github.com/ethpandaops/ethereum-package) know that the created nodes will synch to `devnet-1` of the `uct-finhub-devnets` repository.
        > Example: For the network: `verkle-gen-devnet-7` there is the github repository [verkle-gen-devnets](https://github.com/ethpandaops/verkle-devnets) from the ethpandaops github account.
        
        > There is also a `network-configs` folder which containes the [gen-devnet-7](https://github.com/ethpandaops/verkle-devnets/tree/master/network-configs/gen-devnet-7/metadata) metadata that the ethereum-package will use to bootstrap from and sync the created nodes to.
    - `network_id:` - This is the ID of the UCT Finhub network.
    - `devnet_repo:` - This parameter specifies which github account to search for to find the dev network specified by the `network` parameter.
      - The default account is [ethpandaops](https://github.com/ethpandaops) which runs the `verkle-gen-devnets`.
    - `nat_exit_ip:` - Static IP of the loadbalancer used to access the nodes
    - `checkpoint_sync_enabled:` - This is for the consensus node to sync up to a bootstrap node specified by the end-point `checkpoint_sync_url`.
    - `checkpoint_sync_url:` - URL for the consensus client that will be used for performing a checkpoint sync.
2. To deploy a node on our uct_finhub-devnet-1 network:
   - Run the ethereum kurtosis package as below:
     ```bash
     kurtosis run github.com/ethpandaops/ethereum-package --args-file ./kurtosis_network_params.yaml --image-download always
     ```



