
## Install CAPE

### Try CAPE on Docker-Compose

> Step 1: Clone repo
```
git clone https://github.com/cape-sh/cape-docker
cd cape-docker
docker-compose up -d
```

```
./hacks/config.sh
```
Step 2: Get ipconfig

> For MAC
```
export IP=$(ipconfig getifaddr en0)
```

> For Linux
```
> get the ip address of machine
export IP=$(ip -o route get to 8.8.8.8 | sed -n 's/.*src \([0-9.]\+\).*/\1/p')
```


> Step 3: Install CAPE 
```
export KUBECONFIG=$(pwd)/kubeconfigs/cape.yaml

helm repo add cape https://charts.cape.sh
helm repo update

helm install cape cape/cape  \
--set acceptTOS=true \
--set licence="free10nodes" \
--set ingress.hostname=${IP}.nip.io \
--set ingress.scheme=https

kubectl -n cape wait --for=condition=available --timeout=600s deployment/web
```

> Step 4: Launch browser
```
open https://${IP}.nip.io
```

## Support
For more information on CAPE, return to the main [Repo](https://github.com/cape-sh/cape)

