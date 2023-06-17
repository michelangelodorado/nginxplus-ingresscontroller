# nginxplus-ingresscontroller
<a name="readme-top"></a>
<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

Installing the NGINX Ingress Controller in your Kubernetes cluster using Kubernetes manifests

This project was created based on the documentation below but modifications has been made to use NGINX Plus image from the private repository:<br>
[https://docs.nginx.com/nginx-ingress-controller/installation/installation-with-manifests/](https://docs.nginx.com/nginx-ingress-controller/installation/installation-with-manifests/)

<!-- GETTING STARTED -->
## Getting Started

You will be able to install NGINX Plus Ingress Controller in a Kubernetes cluster using the steps below

This is tested on Azure AKS, using NGINX Plus version 3.1.1


### Prerequisites

* Kubernetes cluster in Azure (AKS) or AWS (EKS)

### Installation

_Below is an example of how you can instruct your audience on installing and setting up your app. This template doesn't rely on any external dependencies or services._

1. Prepare your NGINX Plus JWT token license, you can get a free NGINX Plus trial license at [https://www.nginx.com/free-trial-request/](https://www.nginx.com/free-trial-request/)
2. Clone the repo
   ```sh
   git clone https://github.com/michelangelodorado/nginxplus-ingresscontroller.git
   ```
3. Change your current working directory to the newly cloned repository
   ```sh
   cd nginxplus-ingresscontroller
   ```
4. Run the command below to store contents inside jwt variable
   ```sh
   read jwt
   ```
5. Paste the contents of the `nginx-repo.jwt` you obtained from NGINX Team. For example:
   ```console
   admin@kube-master nginxplus-ingresscontroller % read jwt
   eyJhbGciOiJSUzI1NiIsIn65cCI6IkpXVCIsImtpZCI6InRyaWFsIn0.eyJpc3MiOiJuZ2lueCBpc3N1ZXIiLCJpYXQiOjE2ODU3MjM2NDUsImp0aSI6IjEzMzE5Iiwic3ViIjoiSTAwMDEzMDQwOCIsImV4cCI6MTcwMTI3NTY0NX0.GT1pjWhttF_NpkXC_W0SdyanaM6nPwvv608cKBerqeGUY6WX03h5CjIq9XLgF7b0lfPxLoruyvzf0Jxa8o7w1768CmxFsaHbmv5Z-ueDX3e_s_2oTWGREBw_HwdpM7sJY2XoBd9eMacA7eL5cgSMB9JSOBKEGNm83vM_xuIC1mnfwRNh1qxR2l-bdzj_ErP7rIK7AswApMg2hqOeUbeHYN3og33gL7LhsaKesFeg6t-LA11lVNPN0F2jZ31EV3Q0ZI0ePlCY30y-AZtU92YPYfNpG9ekVEu16UOinKEY6yGpPgPMMsgnvtOEmQZcmnxCqyq54FSRYl3-49PSvZ2W16ic2zZxw67ERwfnHkawQqwigmjW73NYZoQOZyToWvMW6mJ9Lu6dE3L8r66AI9-JO6xH9aUS39BHfFtAzmaewItPRvUgaEtczNQnL5_UnY6xcaRDRPcP4oaEu6S56qKbpXxtfV-OsgRbK7z-uQdCe0jO85H53qbIATlkqUagEKd8
   ```
6. Run the command below to create a secret using the value from jwt
   ```sh
   kubectl create secret docker-registry regcred --docker-server=private-registry.nginx.com --docker-username=$jwt --docker-password=none -n nginx-ingress
   ``` 
7. Configure namespace and service account
   ```sh
   kubectl apply -f ns-and-sa.yaml
   ``` 
8. Configure RBAC
   ```sh
   kubectl apply -f rbac.yaml
   ``` 
9. Create a config map for customizing NGINX configuration<a name="Step 9"></a>
    ```sh
    kubectl apply -f nginx-config.yaml
    ``` 
10. Create an IngressClass resource:
    ```sh
    kubectl apply -f ingress-class.yaml
    ``` 
11. Create custom resource definitions for VirtualServer and VirtualServerRoute, TransportServer and Policy resources:
    ```sh
    kubectl apply -f k8s.nginx.org_virtualservers.yaml
    kubectl apply -f k8s.nginx.org_virtualserverroutes.yaml
    kubectl apply -f k8s.nginx.org_transportservers.yaml
    kubectl apply -f k8s.nginx.org_policies.yaml
    ```
12. Deploy the Ingress Controller
    ```sh
    kubectl apply -f nginx-ingress-deployment.yaml
    ```
13. Create a service using a manifest for your cloud provider:

    * <b>Azure</b>:
      ```sh
      kubectl apply -f nginx-ingress-service.yaml
      ```
    * <b>AWS</b>:
      ```sh
      kubectl apply -f nginx-ingress-service-aws.yaml
      ```
      Add the following keys to the config map file `nginx-config.yaml` from <a href="#Step 9">Step 9</a>
      ```sh
      proxy-protocol: "True"
      real-ip-header: "proxy_protocol"
      set-real-ip-from: "0.0.0.0/0"
      ```
      Update the config map
      ```sh
      kubectl apply -f nginx-ingress-service.yaml
      ```
    
14. Expose the NGINX Ingress Controller Dashboard
    ```sh
    kubectl apply -f dashboard-nginx-ingress-service.yaml
    ```

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- USAGE EXAMPLES -->
## Usage

Use this to quickly deploy NGINX Plus Ingress Controller into your Kubernetes cluster and avoid repeating tasks
<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- ACKNOWLEDGMENTS -->
## Acknowledgments

* [NGINX Ingress Controller - Installation with Manifests](https://docs.nginx.com/nginx-ingress-controller/installation/installation-with-manifests/)

<p align="right">(<a href="#readme-top">back to top</a>)</p>
