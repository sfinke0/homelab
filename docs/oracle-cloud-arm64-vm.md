# k3s on Oracle Cloud ARM VM

```
# install k3s
curl -sfL https://get.k3s.io | INSTALL_K3S_EXEC='--cluster-cidr=100.64.0.0/16 --service-cidr=100.65.0.0/16 --cluster-dns=100.65.53.53 --flannel-backend=none --disable-network-policy --disable "servicelb" --disable "traefik" --disable "metrics-server" ' sh -

export KUBECONFIG=/etc/rancher/k3s/k3s.yaml

# install cilium CLI
CILIUM_CLI_VERSION=$(curl -s https://raw.githubusercontent.com/cilium/cilium-cli/main/stable.txt)
CLI_ARCH=amd64
if [ "$(uname -m)" = "aarch64" ]; then CLI_ARCH=arm64; fi
curl -L --fail --remote-name-all https://github.com/cilium/cilium-cli/releases/download/${CILIUM_CLI_VERSION}/cilium-linux-${CLI_ARCH}.tar.gz{,.sha256sum}
sha256sum --check cilium-linux-${CLI_ARCH}.tar.gz.sha256sum
sudo tar xzvfC cilium-linux-${CLI_ARCH}.tar.gz /usr/local/bin
rm cilium-linux-${CLI_ARCH}.tar.gz{,.sha256sum}

```
