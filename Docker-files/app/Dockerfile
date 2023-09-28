# 建構階段（Maven）
FROM openjdk:11 AS BUILD_IMAGE
RUN apt update && apt install maven -y
RUN git clone https://github.com/ZChungChen/vprofile-project.git
RUN cd vprofile-project && git checkout docker && mvn install

# 運行提交階段
FROM tomcat:9-jre11
LABEL "Project"="Vprofile"
LABEL "Author"="Ryan"
RUN rm -rf /usr/local/tomcat/webapps/* 
COPY --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]