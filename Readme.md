#  Automate Cloud for all : How to integrate the load tests in Dynatrace

In this lab, you will run a jmeter sceanrio to test the demo easytravel application.  
You will need : a free_trial Dynatrace tenant and a linux environment to install easytravel docker and jmeter (easytravel, jmeter and monaco can be on the same host or not)

# Prerequisite : OneAgent and easytravel

1) get your Dynatrace free trial  

      https://www.dynatrace.com/trial/    

2) install dynatrace OneAgent on your host 
([oneagent installation documentation](https://github.com/ace-dynatrace-lab/ace-load-testing-automation/blob/main/InstallEasytravel.md))    

       Go to your Dynatrace free trial > Dynatrace Hub > OneAgent Linux (https://abcd.live.dynatrace.com/#install;gf=all),
       and follow the workflow :
       1)  Download the installer using this command on the target host: 
             wget  -O Dynatrace-OneAgent-Linux-1.xxx.sh ...
       2)  Verify signature (optional)
       3)  Set customized options:
           - host-group => easytravel00 
           - properties => env=sandbox
       4) Run the installer with root rights : 
            sudo /bin/sh Dynatrace-OneAgent-Linux-1.213.155.sh --set-host-group=easytravel00 --set-host-property=env=sandbox

3) install easytravel docker   
- test if easytravel is already installed (it could be the case for the training and quickstart environment)   

      docker ps --format "{{.ID}}\t{{.Status}}\t{{.Names}}"

- if you have this result, you don't need to install easytravel  
  ![image](https://user-images.githubusercontent.com/40337213/116451621-02f57e00-a85d-11eb-96a0-c1d0613185c7.png)
  
      skip this step
            
- if not, install easytravel  

      cd;git clone https://github.com/Dynatrace/easyTravel-Docker;
      cd easyTravel-Docker;
      export ET_APM_SERVER_DEFAULT=APM;
      docker-compose up -d

more info here : https://github.com/Dynatrace/easyTravel-Docker  
  
4) from your browser you can access to easytravel  

       http://<myhostname.domain.com>

5) restart easytravel and stop loadgen  
Go to your dynatrace environment : *Deployment status > OneAgents*, if there is a warning wih the message process **isn't monitored**, you have to restart easytravel. It's the case when the oneagent is installed after the application :  
    <img src="https://user-images.githubusercontent.com/40337213/116455523-713c3f80-a861-11eb-8786-0858aa10512c.png" width="600" height="200">

- restart easytravel docker (without loadgen)

      export ET_APM_SERVER_DEFAULT=APM;
      docker-compose down;
      docker-compose up -d;
      docker-compose stop loadgen
       
  ![image](https://user-images.githubusercontent.com/40337213/116618345-39a3c500-a93f-11eb-9d84-017a0a26ed4c.png)


# Next Step
- [00-start-with-Jmeter](https://github.com/dynatrace-ace-services/easy-loadtesting-integration/tree/main/00-start-with-Jmeter) => to install Jmeter docker and start your firts load test run without Dynatrace integration.
- [01-deploy-config-with-Monaco](https://github.com/dynatrace-ace-services/easy-loadtesting-integration/tree/main/01-deploy-config-with-Monaco) => to prepare the environment with request attribute, etc..
- [02-loadtesting-Integration](https://github.com/dynatrace-ace-services/easy-loadtesting-integration/tree/main/02-loadtesting-Integration) => to run the load test with Dynatrace integration
- [03-results-in-Dynatrace](https://github.com/dynatrace-ace-services/easy-loadtesting-integration/tree/main/03-results-in-Dynatrace) => to analyse the result in Dynatrace
- [04-driven-Slo](https://github.com/dynatrace-ace-services/easy-loadtesting-integration/tree/main/04-driven-Slo) => to define your service level objectifs
- [05-delete-Config](https://github.com/dynatrace-ace-services/easy-loadtesting-integration/tree/main/05-delete-Config) => to clean the environment
- [06-in-Summary](https://github.com/dynatrace-ace-services/easy-loadtesting-integration/tree/main/06-in-Summary) => it's an overview of the task you can easily automate.
- [07-next-Step](https://github.com/dynatrace-ace-services/easy-loadtesting-integration/tree/main/07-next-Step) => now you are ready to integrate Dynatrace configuration to your CICD pipeline.   
    
