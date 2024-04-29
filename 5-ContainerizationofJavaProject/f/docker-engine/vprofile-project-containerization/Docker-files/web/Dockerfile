FROM nginx AS WEBTier
LABEL "Project"="Containerization"
LABEL "Course"="DevOps Skills with Real challenge"

RUN rm -rf /etc/nginx/conf.d/default.conf
COPY nginvproapp.conf /etc/nginx/conf.d/nginvproapp.conf
