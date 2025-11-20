# Kubernetes Module

## Variables

  - `PRDVTY_KUBERNETES_CONFIG_NAMES="kubeconfig"`: List of filenames to look for in the folder hierarchy
  - `PRDVTY_KUBERNETES_KUBECTL_PATHS="$HOME/bin"`: List of paths where to search for kubectl
  - `PRDVTY_KUBERNETES_CONFIG_CHANGEWARN="true"`: Should the script monitor for changes in the kubeconfig file between runs.
  - `PRDVTY_KUBERNETES_CONFIG_CHANGE_ACTION="retry"`: What action should be done upon change of kubeconfig

#### PRDVTY_KUBERNETES_CONFIG_CHANGE_ACTION

Available options:
  - `warn`: Simply display an error message
  - stop: Display an error message (like warn) but block execution of current command (you just have to retry it)
  - `ask`: Prompt a Y/N question whether the command should still be executed


## Fonctions

The module will look for Kubeconfig files, and define the KUBECONFIG accordingly.
It also provides some security features when working in a shared environment, 

## Internals

