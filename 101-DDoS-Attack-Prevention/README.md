# DDoS Protection attack on a Virtual Machine Scenario 
This repository contains DDoS attack detection & prevention on a Virtual Machine <p></p>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAvyanConsultingCorp%2FDDOS-Attack-Prevention%2Fmaster%2F101-DDoS-Attack-Prevention%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/> 
</a>
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2FAvyanConsultingCorp%2FDDOS-Attack-Prevention%2Fmaster%2F101-DDoS-Attack-Prevention%2Fazuredeploy.json" target="_blank">
    <img src="http://armviz.io/visualizebutton.png"/> 
</a>

# Table of Contents
1. [Objectives](#objectives)
2. [Overview](#overview)
3. [Pre-requisites](#prerequisites)
4. [Deploy](#deployment)
5. [Perform Attack](#attack)
6. [Detect Attack](#detect)
7. [Respond/Mitigate](#mitigate)
8. [Configuration validation](#config)

<a name="objectives"></a>
# Objective of the POC  
Showcase DDoS Protection Standard on Azure resources with public IP

# Overview
It showcases following use cases
1. Perform DDoS attack on resources in a virtual network including public IP addresses associated with virtual machines by following configuration --> DDoS Protection Standard detects attack and mitigate the DDoS attack and send alert.
    * Virtual Network (VNet enabled DDoS Protection Standard)

<a name="important-notes"></a>

# Important Notes
DDoS Protection Standard protects resources in a virtual network including public IP addresses associated with virtual machines, load balancers, and application gateways. When coupled with the Application Gateway web application firewall, DDoS Protection Standard can provide full layer 3 to layer 7 mitigation capability.  
Refer [Azure DDoS Protection Standard](https://docs.microsoft.com/en-us/azure/virtual-network/ddos-protection-overview) for more details.



<a name="prerequisites"></a>

# Prerequisites
Access to Azure subscription to deploy following resources

1.  Virtual Machine with Virtual Network
2.  OMS (Monitoring)

<a name="deployment"></a>

# Deploy 
1. Deploy using "Deploy to Azure" button at the top 

Following steps are required to create email alert by metric level

1. Clone Azure quickstart templates repository using

    `git clone https://github.com/Azure/azure-quickstart-templates.git`

3. Open Windows PowerShell (Run as Administrator) and navigate to 101-DDoS-Attack-Prevention directory 
 
    `cd .\azure-quickstart-templates\101-DDoS-Attack-Prevention\`

4. Execute following command to create email alert rule

    `.\DSC\configure-metricrule.ps1 -ResourceGroupName "<ResourceGroupName>" -Location "<location>" -Email "<EmailID>" -Verbose`
    
5. To configure Azure Security Center, pass email address `<email id>` for notification

    `.\DSC\configure-azuresecuritycenter.ps1 -EmailAddressForAlerts <email id>`

6. To create standard DDoS plan and configure with virtual network <br />

    a. Go to Azure Portal --> Click on "Create a resource" --> Search "DDoS Protection  plan"

      ![]()
    
    b. Enter details 

      ![]()

    c. Configure standard DDoS protection plan on VNet

      ![]()


<a name="attack"></a>

# Perform Attack 
 ### * Attack VM without DDoS protection & analyze <br />
Microsoft have partnered with [BreakingPoint Cloud](https://www.ixiacom.com/products/breakingpoint-cloud) to offer tooling for Azure customers to generate traffic load against DDoS Protection enabled public endpoints to simulate TCP SYN flood and DNS flood attack on the VM without DDoS Protection Standard. Create a  support request with [BreakingPoint Cloud](https://www.ixiacom.com/products/breakingpoint-cloud) for simulation of a DDoS attack on infrastructure. The team executed TCP SYN flood and DNS flood attack on the VM without DDoS Protection Standard  <br />

In this case DDoS attack can not be detected as shown in below images. <br />
To monitor from metrics to find public IP is under DDoS attack (Does not detect DDoS attack)  <br />
    Azure Portal-->Resource Group --> VM --> Metrics --> Select below options  <br />
    - Select specific Public IP in resource option   <br />
    - "Under DDoS attack or not" in metrics filter  <br />
    

   ![]()


To monitor from metrics to find public IP inbound packets status (Does not detect DDoS attack) <br />
    Azure Portal-->Resource Group --> VM --> Metrics --> Select below options from metrics filter  <br />
    - inbound packets DDoS  <br />
    - inbound packets dropped DDoS  <br />
    - inbound packets forwarded DDoS  <br />


  ![]()

 ### * Attack on VM with DDoS Protection Standard <br />

Microsoft have partnered with [BreakingPoint Cloud](https://www.ixiacom.com/products/breakingpoint-cloud) to offer tooling for Azure customers to generate traffic load against DDoS Protection enabled public endpoints to simulate TCP SYN flood and DNS flood attack on the VM without DDoS Protection Standard. Create a  support request with [BreakingPoint Cloud](https://www.ixiacom.com/products/breakingpoint-cloud) for simulation of a DDoS attack on infrastructure. The team executed TCP SYN flood and DNS flood attack on the VM with DDoS Protection Standard <br />

    
<a name="detect"></a>
    
<a name="config"></a>