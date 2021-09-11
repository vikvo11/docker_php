docker build -t vikvo11 .

docker tag vikvo11:latest vikvo11/k8sphp:latest

docker push vikvo11/k8sphp:latest

docker run -it -p 1234:80 vikvo11/k8sphp:latest



kubectl get nodes
kubectl get pods

kubectl run hello --generator=run-pod/v1 --image=vikvo11/k8sphp:latest --port=80
kubectl describe pods hello1
kubectl delete pods hello


# google \https://cloud.google.com/sdk/docs/install#linux
# https://console.cloud.google.com/kubernetes/list?organizationId=0&project=stately-avatar-325318
gcloud init
gcloud services enable container.googleapis.com
gcloud compute zones list

--zone=europe-central2-a

gcloud container clusters create vikvo11 --zone=europe-central2-a

gcloud container clusters create vikvo11 --zone=europe-central2-a --num-nodes=3

gcloud container clusters get-credentials vikvo11 --zone=europe-central2-a

gcloud container clusters delete vikvo11 --zone=europe-central2-a

***
#kubectl run hello --generator=run-pod/v1 --image=vikvo11/k8sphp:latest --port=80
kubectl run hello --image=vikvo11/k8sphp:latest --port=80

kubectl exec hello -- date
kubectl exec -it hello 

kubectl exec -it my-web bash
kubectl exec -it my-web date

kubectl apply -f myfile.yml  ## apply manifest file
kubectl delete -f myfile.yml

kubectl logs hello
kubectl port-forward hello 7788:80

#### Deployment

