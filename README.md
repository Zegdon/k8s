# stc-kubernetes

Rendszerkövetelmények

- docker
- kubernetes
- minikube

Backend konténerek fontos parancsok: 

1. mvn clean package
2. docker-compose up 
    - felépíti a konténereket
    - a konténerek kreálása után lekell állítani azokat
    - crtl+c vel leállítjuk a konténereket
3. minikube start --cpus 4 --memory 6144
    - elindítja a minikube-ot 4cpu val és 6 giga memóriával (a default túl kevés az alkalmazásnak ami 2cpu és 2 GB memória)
4. minikube local image-k betöltése a következő parancsokkal:
```
minikube image load mysql:5.7
minikube image load config-service:latest
minikube image load user-service:latest
minikube image load course-service:latest
minikube image load email-service:latest
minikube image load feedback-service:latest
minikube image load filemanagement-service:latest
minikube image load  discovery-service-peer1:latest
minikube image load  discovery-service-peer2:latest	
minikube image load gateway-service:latest
minikube image load task-service:latest
```
minden egyes image-t bekell tölteni cache-be

5. nevter letrehozasa
```
kubectl create namespace stc
```
6. kubectl apply -f .
    - a mappában ahol a deployment fájlok találhatók kell a parancsot futtatni
7. a kezelőfelület megnyitásához
```
minikube dashboard
```


Port forward parancs:

- kubectl -n stc port-forward (pod neve pl:frontend-7c55c8d4f8-hnmvr) 3000:3000 


Frontend:

1. npm install
2. docker build -t frontend --no-cache .  
    - ami létrehozza az image-t 
    - a frontend image -t frontend néven kell menteni így van a deployment fájlban is
3. minikube image load frontend:latest
4. kubectl apply -f .
    - mappában kell futtatni ahol a frontend deployment található


hasznos parancsok
```
curl localhost:8888/user-service/development
```

```
export HOST=user-service:8080
curl -d '{"email":"bob@ross.com","password":"happy123"}' -H "Content-Type: application/json" -X POST http://$HOST/api/user/auth
```

