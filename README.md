# Intelligent-Traffic-Management-System

An Internet connection.

-   Ubuntu\* 20.04 LTS Server.
-   One of the following operating systems:
    - Ubuntu\* 20.04 LTS Server.
    - Lubuntu\* 20.04 LTS.

### Worker Nodes

@@ -58,7 +60,9 @@ control plane host and the worker node host as presented on

-   An Internet connection.

-   Ubuntu\* 20.04 LTS Server.
-   One of the following operating systems:
    - Ubuntu\* 20.04 LTS Server.
    - Lubuntu\* 20.04 LTS.

-   IP camera or pre-recorded video(s).

@@ -109,46 +113,39 @@ In order to run the latest version of Intelligent Traffic Management, you will n

1. Install docker-ce and docker-compose. Run the following commands on both targets:

	- Get gpg key for docker binaries and add the apt repository to your apt source list:
   - Install the latest Docker CLI and Docker daemon by following the Docker
   instructions to [Install using the
   repository](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)
   and [Install Docker
   Engine](https://docs.docker.com/engine/install/ubuntu/#install-docker-engine).

      ```
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

      echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \ $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
      ```
   - Run Docker without sudo following the [Manage Docker as a non-root
   user](https://docs.docker.com/engine/install/linux-postinstall/)
   instructions.

	- Install Docker packages:
      ```
      sudo apt-get update && sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
      ```
   - If your hosts are running behind a HTTP/S proxy server, perform these
   steps. If not, you can skip this step.

	- Configure Docker service:
	In your Docker daemon json ``/etc/docker/daemon.json`` file add the following:
       - Configure proxy settings for the Docker\* client to connect to
          internet and for containers to access the internet by following
          [Configure Docker to use a proxy server](https://docs.docker.com/network/proxy/).

       - Configure proxy settings for the Docker\* daemon by following
          [HTTP/HTTPS proxy](https://docs.docker.com/config/daemon/systemd/#httphttps-proxy).

   - Install the docker-compose tool by following [Install Compose](
   https://docs.docker.com/compose/install/#install-compose).

   - Configure the Docker service by adding the following to the
	``/etc/docker/daemon.json`` file:

      ```
         "exec-opts": [
               "native.cgroupdriver=systemd"
         ],
         "default-ulimits": {
               "nofile": {
                  "Name": "nofile",
                  "Hard": 65535,
                  "Soft": 65535
               },
               "nproc": {
                  "Name": "nproc",
                  "Hard": 4096,
                  "Soft": 4096
               }
            }
      ```
	- Configure Docker service proxy.
	Update Docker service no proxy settings configuration on the following proxy configuration files: ``/etc/systemd/system/docker.service.d/https-proxy.conf`` and ``/etc/systemd/system/docker.service.d/http-proxy.conf``:
      ```
      NO_PROXY="PREVIOUS_NO_PROXY, CONTROL_PLANE_IP, WORKER_IP"
         {
             "exec-opts": [
                 "native.cgroupdriver=systemd"
             ]
         }
      ```
	- Both machines should have no_proxy set to controller_plane_ip and worker_ip
	- Run `sudo systemctl daemon-reload and sudo systemctl restart docker.service` to apply changes.


2. Install Helm. Run the following commands on both targets:
@@ -190,7 +187,7 @@ In order to run the latest version of Intelligent Traffic Management, you will n
	sudo kubeadm init --pod-network-cidr=10.244.0.0/16
    ```

    >**NOTE:** Save the kube join command prompted a the end of the cluster creation
    >**NOTE:** Save the kube join command prompted at the end of the cluster creation.

5. Configure access to Kubernetes cluster:
@@ -233,7 +230,7 @@ In order to run the latest version of Intelligent Traffic Management, you will n
    ```

8. Join Kubernetes worker node:
	- If you didn't save the join command in step 5, run the following command on the control plane to generate another token. (If you have the join command, skip this step.)
	- If you didn't save the join command in step 4, run the following command on the control plane to generate another token. (If you have the join command, skip this step.)

       ```
      kubeadm token create --print-join-command
@@ -314,8 +311,8 @@ it.
[Configure &
Download](https://software.intel.com/iot/edgesoftwarehub/download/home/ri/intelligent_traffic_management)

1.  Make sure that the Target System Requirements are met properly
    before proceeding further.
1.  Make sure that the [Target System Requirements](#target-system-requirements)
    are met properly before proceeding further.


2.  If you are behind a proxy network, please ensure that proxy addresses are configured in the system:
@@ -872,7 +869,7 @@ resources:

-   [Intel® Distribution of OpenVINO™ toolkit
    documentation](https://docs.openvinotoolkit.org/2021.1/index.html)
-   [Intel® DL Streamer documentation ](openvinotoolkit.github.io/dlstreamer_gst/index.html)
-   [Intel® DL Streamer documentation ](https://docs.openvino.ai/latest/openvino_docs_dlstreamer.html#doxid-openvino-docs-dlstreamer)

## Troubleshooting
