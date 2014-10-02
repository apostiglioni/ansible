FROM ansible/ubuntu14.04-ansible:stable

ADD aem-6.0-quickstart.jar /opt/aem/aem-6.0-quickstart.jar
ADD license.properties     /opt/aem/license.properties
ADD aem-6-starter          /opt/aem/docker-starter \
 && chmod    0744          /opt/aem/docker-starter \
 && chown aem:aem          /opt/aem/docker-starter

RUN useradd aem -U
USER aem
WORKDIR /home/aem

RUN git clone https://github.com/apostiglioni/ansible -b wip --depth 1
ADD aem.yml                /home/aem/ansible/aem.yml
ADD local              	   /home/aem/ansible/local

RUN ansible-playbook aem.yml \
    -i localhost \
    --extra-vars "aem_quickstart_jar=/opt/aem/aem-6.0-quickstart.jar aem_license_file=/opt/aem/license.properties" \
    --connection=local
