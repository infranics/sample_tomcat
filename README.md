
1) https://tomcat.apache.org/tomcat-8.0-doc/appdev/sample/ 에서 sample.war
다운로드

2) sample.war를 사용하는 tomcat Dockerfile 작성

$ cat Dockerfile

FROM tomcat:8.5.97-jdk8
         
ADD sample.war /usr/local/tomcat/webapps/ROOT.war
 
CMD ["catalina.sh", "run"]

3) docker image 생성

$ docker build --no-cache --tag infranics/sample_tomcat:0.1 .

...

=> [2/2] ADD sample.war /usr/local/tomcat/webapps/ROOT.war                                                        0.5s

=> exporting to image                                                                                             0.0s

=> => exporting layers                                                                                            0.0s

=> => writing image sha256:532501ed54c83142fd6f1961428e7c8211875917c9981770fa062cf7f92d7f40                       0.0s

=> => naming to infranics/sample_tomcat:0.1                                                         0.0s

$ docker images

REPOSITORY                                                    TAG              IMAGE ID       CREATED         SIZE

infranics/sample_tomcat                                       0.1              532501ed54c8   6 seconds ago   338MB

4) sample_tomcat 이미지 dockerhub 업로드

$ docker push infranics/sample_tomcat:0.1

5) sample_tomcat_deployment.yml 수정 및  배포 

$ kubectl apply -f sample_tomcat_deployment.yml

6) sample_tomcat_svc.yaml 수정 및  배포

$ kubectl apply -f sample_tomcat_svc.yaml

