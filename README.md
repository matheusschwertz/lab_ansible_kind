# Criação de um Cluster KIND com Gerenciamento usando Ansible

Este guia descreve como criar um cluster Kubernetes local utilizando o KIND (Kubernetes IN Docker) e como utilizar o Ansible para executar tarefas de gerenciamento nesse cluster.

## Pré-requisitos

- Docker instalado no seu sistema
- Ansible instalado no seu sistema

## Instalação do KIND

Siga as instruções para instalar o KIND em: [https://kind.sigs.k8s.io/docs/user/quick-start/](https://kind.sigs.k8s.io/docs/user/quick-start/)

## Configuração do Cluster KIND

Use um arquivo YAML de configuração (por exemplo, `cluster-config.yaml`) para definir as propriedades do seu cluster:

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
  kubeadmConfigPatches:
  - |
    kind: InitConfiguration
    nodeRegistration:
      kubeletExtraArgs:
        node-labels: "ingress-ready=true"
- role: worker
- role: worker
