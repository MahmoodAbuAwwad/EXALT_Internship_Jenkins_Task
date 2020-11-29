we need 2 machines or 
as required we need 2 docker containers :))



first one need to be jenkins container
and the other we need to create another tiny vm with our docker image from our dockerfile embedded with ssh service

1-mkdir and cd to it

2- first use ssh-keygen to generate new ssh key
	ssh-keygen -f root-key

it will create 2 root-key in same dir public/private

3- write docker file
dockerfile have some imporntant comments
