# **Environment Setup**

## **vscode + docker + ubuntu18.04 + ssh**
******

## **Download software**

- docker

- vscode

## **Setup ubuntu in Docker**

- pull ubuntu 18.04 image from docker

    ```properties
    docker pull ubuntu:18.04
    ```

- create container from image

    <!-- ```properties
    docker container run -it -p 7777:22 -v /Users/{username}/Desktop/{csapp_desktop}:/{csapp_container} --name={container_name} ubuntu:18.04
    ``` -->

    <!-- my environment setup:  -->

    ```properties
    docker container run -it -p 7777:22 -v /Users/zoey/Desktop/csapp_labs:/csapp_labs --name=csapp_env ubuntu:18.04
    ```

- connect to docker:

    ```properties
    docker exec -it csapp_env /bin/bash
    ```

- update and install

    ```properties
    apt-get update
    ```

    ```properties
    apt-get install sudo
    ```

    ```properties
    sudo apt-get install -y build-essential gcc-multilib gdb openssh-server vim
    ```

## **Setup ssh in Docker**

- open ssh_config in vim

    ```properties
    vim /etc/ssh/sshd_config
    ```

- uncomment the lines:

    ```properties
    Port 22
    PermitRootLogin yes
    PubkeyAuthentication yes
    AuthorizedKeysFile      .ssh/authorized_keys .ssh/authorized_keys2
    ```

- restart ssh 

    ```properties
    service ssh restart
    ```

## **Auto restart ssh**

- open startup_run script in vim

    ```properties
    vim /root/startup_run.sh
    ```

- add content

    ```properties
    #!/bin/bash

    LOGTIME=$(date "+%Y-%m-%d %H:%M:%S")
    echo "[$LOGTIME] startup run..." >>/root/startup_run.log
    service ssh start >>/root/startup_run.log
    ```

- update file permissions

    ```properties
    chmod +x /root/startup_run.sh
    ```

- open .bashrc in vim

    ```properties
    vim /root/.bashrc
    ```

- add content to end of file

    ```properties
    #startup run
    if [ -f /root/startup_run.sh ]; then
        /root/startup_run.sh
    fi
    ```

- import the update to .bashrc file

    ```properties
    source ~/.bashrc
    ```

- change password for root

    ```properties
    sudo passwd root
    ```

## **Setup ssh in vscode**

- install remote ssh extension

- search or ctr+shift+p, type `remote-ssh`, choose `open Configuration file`

- add config for csapp_env

    ```properties
    Host csapp_env
        HostName 127.0.0.1
        User root
        Port 7777
    ```

- solution for rebuild container and update ssh in host

    ```properties
    vim .ssh/known_hosts
    ```
