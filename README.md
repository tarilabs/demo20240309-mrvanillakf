Deployed a vanilla KF in Minikube (or else)

Remember to verify:
```
sudo sysctl fs.inotify.max_user_instances=2280
sudo sysctl fs.inotify.max_user_watches=1255360
minikube start
minikube dashboard
```

# port fwd checklist
```
kubectl port-forward svc/istio-ingressgateway -n istio-system 8080:80
kubectl port-forward svc/minio-service -n kubeflow 9000:9000
```

Connect to cluster: https://github.com/kubeflow/manifests?tab=readme-ov-file#connect-to-your-kubeflow-cluster

Deployed `poddefault.yaml`

Deployed `/servingruntime-model-server.yaml`

Used at the time of writing:
- `kubeflownotebookswg/jupyter-tensorflow-full:v1.8.0-rc.6`
- cpu 8
- ram 16
- mounted poddefault for miniosecret


# Model Registry
```
kubectl apply -k manifests/kustomize/overlays/db
kubectl apply -k manifests/kustomize/options/istio
kubectl port-forward svc/model-registry-service -n kubeflow 8081:8080
```

```
curl -s -X 'GET' \
  'http://localhost:8081/api/model_registry/v1alpha2/registered_models?pageSize=100&orderBy=ID&sortOrder=DESC' \
  -H 'accept: application/json' | jq
```
