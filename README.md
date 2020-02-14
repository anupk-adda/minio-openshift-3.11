# minio-openshift-3.11
deployment step for minio on openshift

Preqisite :
-A existing cluster with openshift 3.11
- oc tools on your client machine.

Step 1 .login to your openshift cluster 
Step 2. oc create -f https://raw.githubusercontent.com/minio/minio-operator/master/minio-operator.yaml


This will create all relevant resources required for the Operator to work. Here is a list of resources created by above yaml file:
Namespace: Custom namespace for MinIO-Operator. By default it is named as minio-operator-ns.
CustomResourceDefinition: Custom resource definition named as minioinstances.miniocontroller.min.io.
ClusterRole: A cluster wide role for the controller. It is named as minio-operator-role. This is used for RBAC.
ServiceAccount: Service account is used by the custom controller to access the cluster. Account name by default is minio-operator-sa.
ClusterRoleBinding: This cluster wide binding binds the service account minio-operator-sa to cluster role minio-operator-role.
Deployment: Deployment creates a pod using the MinIO-Operator Docker image. This is where the custom controller runs and looks after any changes in custom resource.


Step 3. Change to the project where you want to deploy the minio instance .

you can create MinIO instances using the below command
oc create -f https://raw.githubusercontent.com/minio/minio-operator/master/examples/minioinstance.yaml

step 4. Enable the route to the minio-hl-svc 
oc expose svc/minio-hl-svc

step 5. get the routes using below command
oc get routes

step 6. login to the minio browser using the credential
accesskey : minio 
secretkey : minio123

