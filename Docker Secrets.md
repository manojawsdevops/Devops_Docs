cd manoj/
   
     vi pass.txt
     ls
     docker secret --help
     docker secret create dbpass
     docker secret create name pass.txt 
     docker inspect dbpass pass
 In cli
   echo "sarasu10" | docker secret create dbpass -
   docker service create --name redis  --secret manoj redis:alpine
   docker service ls

