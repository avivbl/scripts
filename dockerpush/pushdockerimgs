#!/bin/bash
read -p "How many Docker images? " IMGS_COUNT
IMGS_COUNT=1000
i="0"

while [ $i -lt $IMGS_COUNT ]
do
  MYVAR=`cat /dev/urandom | tr -dc 'a-z' | fold -w 2 | head -n 1`
  echo "Random letters are $MYVAR"
  
  echo "i is $i"
  MYRAND=$(((RANDOM%10)+1))
  
  img=`sudo docker search $MYVAR | awk 'NR>'$MYRAND'{print $1}' | awk 'NR<2{print $1}'`
  echo "Pulling $img"
  sudo docker pull $img;
  sudo docker tag $img 10.166.0.4:8081/docker-local/$img;
  echo "Pushing $img"
  sudo docker push 10.166.0.4:8081/docker-local/$img;
  sudo docker rmi 10.166.0.4:8081/docker-local/$img;
  sudo docker rmi $img;
  echo "Finished pushing $img"
  i=$[$i+1]
  
done
