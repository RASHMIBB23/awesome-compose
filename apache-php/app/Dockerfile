#synatax=docker /dockerfile:1.4
#base image with ohp 8.09 and apache
FROM --platform=$BUILDPLATFORM php:8.0.9-apache as builder
#set default command to keep apache running
CMD ["apache2-foreground"]
#create the new build stage for development tools
FROM builder as dev-envs

#updata package list and install github list
RUN apt-get update && apt-get install -y --no-install-recommends git \
&& apt-get clean && rm -rf /var/lib/apt/lists/*

#crate a new user 'vscode' with a hoe directory and bash shell
RUN useradd -s /bin/bash -m vscode
#create the docker code and add the vscode into it user into it
RUN groupadd -f docker && usermod -aG docker vscode
#COPY Docker tools(CLI,BUildx,Compose) vfrom an external image
COPY --from=gloursdocker/docker / /

#ensure apache runs in the foreground when the conatins starts
CMD ["apach2"]
