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
   
## 02. Storage Volume

   - ### 02.01. Create EmptyDir volume
      ```t
         apiVersion: v1
         kind: Pod
         metadata:
           name: test-nginx
         spec:
           containers:
           - image: nginx
             name: test-nginx
             volumeMounts:
             - mountPath: /cache
               name: cache-volume
           volumes:
           - name: cache-volume
             emptyDir: {}


         ## Create & Display EmptyDir volume

         Let's try K8 : kubectl apply -f emptydir.yml
         pod/test-nginx created

         Let's try K8 : kubectl get pods
         NAME         READY   STATUS    RESTARTS   AGE
         test-nginx   1/1     Running   0          7s

         Let's try K8 : kubectl exec -it test-nginx -- /bin/bash
         root@test-nginx:/# mount | grep -i cache
         /dev/vda1 on /cache type ext4 (rw,relatime)
         
         kubectl describe pod test-nginx
         kubectl delete po test-nginx

      ```
 
   - ### 02.02. Create HostPath volume
      ```t
       kubectl create -f hostpath-test.yaml
       kubectl get po
       kubectl exec redis-hostpath df /test-mnt
       kubectl delete po redis-hostpath
      ```
         - ### HostPath - From HOST to Pod : (Node2)
               ```t
               cd /test-vol
                echo "From host" > from-host.txt
                cat from-host.txt
               ```
         - ### Pod (Master)
               ```t
                kubectl exec redis-hostpath cat /test-mnt/from-host.txt
                echo "From host" > from-host.txt
                cat from-host.txt
                kubectl exec redis-hostpath -it -- /bin/sh
                cd /test-mnt
                echo "test host" > from-pod.txt
                cat from-pod.txt
               ```
          - ### HostPath - From HOST to Pod : (Node2)
            ```t
            cd /test-vol
            ls
            cat from-pod.txt
            ```
