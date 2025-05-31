# settings_k8s

# Calico: - https://docs.tigera.io/calico/latest/getting-started/kubernetes/self-managed-onprem/onpremises
kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.30.1/manifests/operator-crds.yaml

kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.30.1/manifests/tigera-operator.yaml

kubectl create -f custom-resources.yaml

# MetalLB: - https://metallb.io/installation/
kubectl edit configmap -n kube-system kube-proxy

apiVersion: kubeproxy.config.k8s.io/v1alpha1

kind: KubeProxyConfiguration

mode: "ipvs"

ipvs:

  strictARP: true

kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.14.9/config/manifests/metallb-native.yaml

kubectl apply -f metallb.yaml

# Ingress - Nginx: - https://kubernetes.github.io/ingress-nginx/deploy/#bare-metal-clusters

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.12.2/deploy/static/provider/baremetal/deploy.yaml
