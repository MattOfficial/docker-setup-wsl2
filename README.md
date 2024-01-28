# docker-setup-wsl2

1. Set up WSL2 on windows. Follow this [guide](https://petri.com/how-to-install-wsl-on-windows-server/).
2. Install [VSCode](https://code.visualstudio.com/) and install [docker extension for VSCode](https://code.visualstudio.com/docs/containers/overview).
3. Update and upgrade the repos on Ubuntu.
    ```
    sudo apt update && sudo apt upgrade
    ```
4. Trust the repo:
    ```
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```
5. Update the package repository configuration:
    ```
    echo "deb [arch=amd64] https://download.docker.com/linux/ubuntu jammy stable" | sudo tee /etc/apt/sources.list.d/docker.list
    ```
6. Update and upgrade repos on ubuntu:
    ```
    sudo apt update && sudo apt upgrade
    ```
7. Install official docker release
    ```
    sudo apt install docker-ce docker-ce-cli containerd.io
    ```
8. Add users to docker group:
    ```
    sudo usermod -aG docker $USER
    ```
9. Install net-tools if not installed:
    ```
    sudo apt install net-tools
    ```
10. Get the IP address in ubuntu:
    ```
    echo `ifconfig eth0 | grep -E "([0-9]{1,3}.){3}[0-9]{1,3}" | grep -v 127.0.0.1 | awk '{ print $2 }' | cut -f2 -d:`
    ```
11. Start dockerd
    ```
    sudo dockerd -H unix:///var/run/docker.sock --bip <ip from step 10>/16
    ```
12. Add your docker volume:
    ```
    docker create -it --name my-container --hostname my-host -v docker-dev:/home ubuntu
    ```

Need to check step 10 onwards in windows server.
