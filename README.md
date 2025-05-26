To push from local to ACR
create an image(Refer the Dockerfile)
    docker build -t dotnetwithdockersetup:v1.0.0 .    
Run the image in local container -d mean run service detached,-e environment ,-p port info
    docker run -p 5632:8080 -e ASPNETCORE_ENVIRONMENT=Development --name app-v1.3.0 -d dotnetwithdockersetup:v1.0.0

Push the image to acr
    az acr build --registry acrcloudtechram-b6huexbya5dgfaa7.azurecr.io --image dotnetwithdockersetup:v1.0.0 .

Other useful commands for local
    docker stop app-v1.3.0
    docker start app-v1.3.0
    docket image list
    az login

from local if you want to deploy the image to aks
    az login 
    az aks get-credentials --name CloudTech --resource-group learnRG --overwrite-existing
    az aks update -n CloudTech -g learnRG --attach-acr acrcloudtechram-b6huexbya5dgfaa7.azurecr.io
    az acr build --registry acrcloudtechram-b6huexbya5dgfaa7.azurecr.io --image cloudtechramreg.azurecr.io/dotnetwithdockersetup:v1.0.0 .
Use below cmds for local kubernet 
    az aks install-cli
    az aks get-credentials --name <cluster-name> --resource-group <resource-group>
    az aks get-credentials --name webappaks --resource-group webappaks_group --overwrite-existing
    az aks update -n webappaks -g webappaks_group --attach-acr cloudtechramreg
    kubectl create deployment dep1 --image=cloudtechramreg.azurecr.io/dotnetwithdockersetup:67 --replicas=1
    kubectl get deployment
    kubectl get pods
    kubectl expose deployment dep1 --type=LoadBalancer --port=80 --target-port=8080
debug cmds
    kubectl get svc
    kubectl describe svc dep1
    kubectl get pods
    kubectl logs <pod-name>

