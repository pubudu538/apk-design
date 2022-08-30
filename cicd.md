# CI CD

## Simplest option 

- CP and DP in a single K8s cluster (CP and DP can be in two different or same namespace)
- CP and DP in two different K8s cluster

Prerequisites - Add the data plane environment into kubectl.

1. Add ENV

apkcli add env dev \
--control-plane  https://apim.com:9443 \
--data-plane-context K8S_CONTEXT_NAME

2. Export API 

apkcli export api-product API_NAME -v 1.0.0 -e dev
apkcli export api API_NAME -v 1.0.0 -e dev --namespace wso2

Optional: apkcli export api-product API_NAME -v 1.0.0 -e dev --include-api
(This downloads the DP artifact as well)

3. Import API

apictl import api-product -f ./PATH_TO_API_PRODUCT -e dev 
apictl import api -f ./PATH_TO_API -e dev --namespace wso2


## Advanced Use Cases 

Single CP and multiple DP K8s Clusters

Prerequisites - Add the data plane environment into kubectl.

1. Add ENV

apkcli add env dev \
--control-plane  https://apim.com:9443 \
--data-plane-context K8S_CONTEXT_NAME \
--data-plane-1-context K8S_CONTEXT_NAME_1 \
--data-plane-2-context K8S_CONTEXT_NAME_2 \

2. Export API 

apkcli export api-product API_NAME -v 1.0.0 -e dev
apkcli export api API_NAME -v 1.0.0 -e dev.dp0 --namespace wso2
apkcli export api API_NAME -v 1.0.0 -e dev.dp1 --namespace wso2

3. Import API

apictl import api-product -f ./PATH_TO_API_PRODUCT -e dev 
apictl import api -f ./PATH_TO_API -e dev.dp0 --namespace wso2
apictl import api -f ./PATH_TO_API -e dev.dp1 --namespace wso2


## Single CP and multiple DPs in a single K8s cluster

Prerequisites - Add the data plane environment into kubectl.

1. Add ENV

apkcli add env dev \
--control-plane  https://apim.com:9443 \
--data-plane-context K8S_CONTEXT_NAME \

2. Export API 

apkcli export api-product API_NAME -v 1.0.0 -e dev
apkcli export api API_NAME -v 1.0.0 -e dev --namespace wso2
apkcli export api API_NAME -v 1.0.0 -e dev --namespace wso2-1

3. Import API

apictl import api-product -f ./PATH_TO_API_PRODUCT -e dev 
apictl import api -f ./PATH_TO_API -e dev --namespace wso2
apictl import api -f ./PATH_TO_API -e dev --namespace wso2-1
