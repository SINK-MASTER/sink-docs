```shell script
DOCKERFILE_PATH=docker
REGISTRY_URL=127.0.0.1:1180
IAMGE_NAME=webapp/sink-web
CONTAINER_NAME=sale-usercenter
LAST_VERSION=$(date +%Y%m%d%H%M%S)
echo '>>> remove old containers'
docker login -u admin -p Sink1234 $REGISTRY_URL

if docker ps -a | grep $IMAGE_NAME; then
    docker rm -f $(docker ps -a | grep $IMAGE_NAME | awk '{print $1}')
fi
echo '>>> remove old image'
#if docker images -a | grep $IAMGE_NAME; then
#    docker rmi -f $(docker images -a | grep $IMAGE_NAME | awk '{print $3}')
#fi
cd /home/jenkins/workspace/sink-web
project_path=$(cd `dirname $0`; pwd)
echo $project_path

cp -rf $DOCKERFILE_PATH/Dockerfile .

echo '>>> build new image'
docker build -t $REGISTRY_URL/$IAMGE_NAME:$LAST_VERSION .
echo '>>> push image to registry'
docker push $REGISTRY_URL/$IAMGE_NAME:$LAST_VERSION
echo '>>> build end'
```