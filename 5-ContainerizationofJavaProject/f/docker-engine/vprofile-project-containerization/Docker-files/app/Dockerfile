# BUILDING THE ARTIFACTS
# To install maven we need JDK https://hub.docker.com/_/openjdk
FROM openjdk:11-jdk AS BUILD_IMAGE
LABEL "Project"="Containerization"
LABEL "Course"="DevOps Skills with Real challenge"
# First update the JDK then install maven for Artifacts
RUN apt update && apt install maven -y
# Now download the project
RUN git clone https://github.com/devopshydclub/vprofile-project.git
# Switch WD to files location then build the artifacts
RUN cd vprofile-project && git checkout docker && mvn install 

# Now we have artifacts and we don't need remainings that's why we are using multi-stage build
# Our app container need Tomcat for application
FROM tomcat:9-jre11 AS Application
# To avoid read-only errors we are giving the -rf option and remove the unnecessary files
# We know that default Tomcat app is runnig under this directory thanks to docker-hub image page
RUN rm -rf /usr/local/tomcat/webapps/*
# Copy the builded artifacts to default directory
COPY --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war 
EXPOSE 8080
#Go to the https://hub.docker.com/_/tomcat link and you will see that Run the default Tomcat server command is CMD ["catalina.sh", "run"] 
CMD ["catalina.sh", "run"]  
