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

This project was created based on the documentation below but modifications has been made to use NGINX Plus image:<br>
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
4. Enter your API in `config.js`
   ```sh
   read jwt
   ```
5. Run the command below to store contents inside 'jwt' variable
   ```sh
   read jwt
   ```
6. Paste the contents of the `nginx-repo.jwt` you obtained from NGINX Team
   ```sh
   read jwt
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
