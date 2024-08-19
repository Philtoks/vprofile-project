FROM openjdk:11 AS maven
RUN apt update 
RUN apt install maven -y
RUN git clone -b main https://github.com/devopshydclub/vprofile-project.git
RUN cd vprofile-project
RUN git checkout docker
RUN mvn install

FROM tomcat:9-jre11
WORKDIR /usr/local/tomcat/webapps/
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=maven vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]