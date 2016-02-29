# postfix
Simple Postfix SMTP TLS relay [docker](http://www.docker.com) image with no local authentication enabled (to be run in a secure LAN). 

### Build instructions

Clone this repo and then:

    cd postfix
    sudo docker build -t postfix .


### How to run it

The following env variables need to be passed to the container:

* `SMTP_SERVER` Server address of the SMTP server to use.
* `SMTP_USERNAME` Username to authenticate with.
* `SMTP_PASSWORD` Password of the SMTP user.
* `SMTP_HOSTNAME` Server hostname for the Postfix container. Emails will appear to come from the hostname's domain.

To use this container from anywhere, the 25 port needs to be exposed to the docker host server:

    docker run -d --name postfix -p "25:25"  \ 
           -e SMTP_SERVER=smtp.bar.com \
           -e SMTP_USERNAME=foo@bar.com \
           -e SMTP_PASSWORD=XXXXXXXX \
           -e SMTP_HOSTNAME=helpdesk.mycompany.com \
           hasgeek/postfix
    
If you are going to use this container from other docker containers then it's better to just publish the port:

    docker run -d --name postfix -P \
           -e SMTP_SERVER=smtp.bar.com \
           -e SMTP_USERNAME=foo@bar.com \
           -e SMTP_PASSWORD=XXXXXXXX \
           -e SMTP_HOSTNAME=helpdesk.mycompany.com \
           hasgeek/postfix

