# building Master(jenkins) and Slave(centosMachine) using Docker

in centos7/Dockerfile --> give the image of centos with openssh installed
and

I create a new user called remote_user on the machinee......


then build services-> jenkins and remote_host
docker-compose build --> to build remote host image
docker-compose up -d --> to start containers 


to make sure we can access via ssh


go inside jenkins (master) container
docker exec -it jenkins bash


do
ssh remote_user@remote_host and provide pass "root"
