docker build -t vikvo11 .

docker tag vikvo11:latest vikvo11/k8sphp:latest

docker push vikvo11/k8sphp:latest

docker run -it -p 1234:80 vikvo11/k8sphp:latest
