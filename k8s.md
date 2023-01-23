# 02. Create Replication controller 

### 01. Create & Display :

   ```t
     kubectl create -f nginx-rc.yaml
     kubectl get pods
     kubectl get po -l app=nginx-app
     kubectl get rs nginx-rc -o wide
   ```

### 02. Describe 

   ```t
    kubectl describe rs nginx-rc
   ```

### 03. Update deployment
   ```t
  kubectl set image deploy nginx-deployment nginx-container=nginx:1.9.1
   kubectl rollout status deploy/nginx-deployment
   kubectl get deploy
   ```
## 06. IF NODE FAIL :

   ```t
     kubectl get po -o wide
    kubectl get nodes
     kubectl get po -o wide

   ```
## 07. Scaling UP :

   ```t
     kubectl scale rs nginx-rc --replicas=5
     kubectl get rs nginx-rc
     kubectl get po -o wide
   ```

## 08. Scaling Down :
   ```t
     kubectl scale rs nginx-rs --replicas=4
     kubectl get rs nginx-rc
     kubectl get po -o wide

   ```


## 07. Delete Replicatoin Controller :
   ```t
     kubectl delete -f nginx-rc.yaml
     kubectl get rs
     kubectl get po -l app=nginx-app
   ```
   



# 03. Create k8s Deployment

### 01. Create & Display :

   ```t
    kubectl create -f nginx-deployment.yaml
    kubectl get deploy
    kubectl get deploy -l app=nginx-app
    kubectl get rs -l app=nginx-app
    kubectl get po -l app=nginx-app
   ```

### 02. Describe 

   ```t
    kubectl describe deploy nginx-deployment
   ```

### 03. Update deployment
   ```t
  ## kubectl set image deploy nginx-deployment nginx-container=nginx:1.9.1
  ## kubectl rollout status deploy/nginx-deployment
  ## kubectl get deploy
   ```


## 05. Rollback 
   ```t
    ## kubectl set image deploy nginx-deployment nginx-container=nginx:1.91 --record
    ## kubectl rollout status deploy/nginx-deployment
    ## kubectl rollout history deploy/nginx-deployment
    ## kubectl rollout undo deploy/nginx-deployment
    ## kubectl rollout status deploy/nginx-deployment

   ```
## 06. IF NODE FAIL :

   ```t
    ## kubectl get po -o wide
    ## kubectl get nodes
    ## kubectl get po -o wide
   ```
## 07. Scaling UP :

   ```t
    ## kubectl scale deployment nginx-deployment --replicas=5
    ## kubectl get deploy
    ## kubectl get po -o wide
   ```


## 08. Scaling Down :
   ```t
    ## kubectl scale deployment nginx-deployment --replicas=2
    ## kubectl get deploy
    ## kubectl get po -o wide
    ## kubectl get po -l app=nginx-app
   ```


## 09. Delete Replicatoin Controller :
   ```t
    ## kubectl delete -f nginx-deployment.yaml
    ## kubectl get rs
    ## kubectl get po -l app=nginx-app
   ```
