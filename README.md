Deployed a vanilla KF in Minikube (or else)
Connect to cluster: https://github.com/kubeflow/manifests?tab=readme-ov-file#connect-to-your-kubeflow-cluster

Deployed `poddefault.yaml`

Used at the time of writing:
- `kubeflownotebookswg/jupyter-tensorflow-full:v1.8.0-rc.6`
- cpu 8
- ram 16
- mounted poddefault for miniosecret

# Model Registry
```
kubectl apply -k manifests/kustomize/overlays/db
kubectl apply -k manifests/kustomize/options/istio
```

# port fwd checklist
```
kubectl port-forward svc/istio-ingressgateway -n istio-system 8080:80
kubectl port-forward svc/minio-service -n kubeflow 9000:9000
```
