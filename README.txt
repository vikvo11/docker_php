docker build -t vikvo11 .

docker tag vikvo11:latest vikvo11/k8sphp:latest

docker push vikvo11/k8sphp:latest

docker run -it -p 1234:80 vikvo11/k8sphp:latest



kubectl get nodes
kubectl get pods

kubectl run hello --generator=run-pod/v1 --image=vikvo11/k8sphp:latest --port=80
kubectl describe pods hello1
kubectl delete pods hello

---GKE Google Kubernetes Engine

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

kubectl create deployment vikvo-deployment --image=vikvo11/k8sphp:latest
kubectl describe pods vikvo-deployment-747d5df774-b8c8m

kubectl describe deploy vikvo-deployment

kubectl scale deployment vikvo-deployment --replicas 4
kubectl get deploy

kubectl get rs # replica set

kubectl delete pods vikvo-deployment-747d5df774-xzxtv

kubectl autoscale deployment vikvo-deployment --min=4 --max=6 --cpu-percent=80
#hpa - horizontal pod autoscale
kubectl get hpa

#### update
kubectl rollout history deployment/vikvo-deployment
kubectl rollout status deployment/vikvo-deployment

kubectl set image deployment/vikvo-deployment k8sphp=adv4000/k8sphp:version1 --record
#rollback to 1 version before
kubectl rollout undo deployment/vikvo-deployment
#
kubectl rollout undo deployment/vikvo-deployment --to-revision=4

kubectl rollout restart deployment/vikvo-deployment

####Manifest for deployment
kubectl apply -f deploy-1-simple.yaml

kubectl delete deployment --all
kubectl delete hpa --all
kubectl delete rs --all

#Services
--ClusterIP
 kubectl create deployment vikvo-deployment --image vikvo11/k8sphp:latest
 kubectl scale deployment vikvo-deployment --replicas 3
 kubectl expose deployment vikvo-deployment --type=ClusterIP --port 80
 kubectl get service /kubectl get svc
 >> SSH to node -> curl 10.3.247.251
 kubectl delete service vikvo-deployment
 --NodePort
 kubectl expose deployment vikvo-deployment --type=NodePort --port 80
 kubectl get service
 kubectl describe nodes |grep ExternalIP
 gcloud compute instances list
 --FIREWALL!!!
 gcloud compute firewall-rules create myservice --allow tcp:31045
 
 kubectl delete svc vikvo-deployment
 --LoadBalancer
 kubectl expose deployment vikvo-deployment --type=LoadBalancer --port 80
 kubectl delete svc vikvo-deployment
 kubectl delete deployment vikvo-deployment
 kubectl get pods
 
