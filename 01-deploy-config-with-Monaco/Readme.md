# 01-deploy-config-with-Monaco

In this step, we will use monaco to import these configurations :  
- Auto-Tag : **front** => to tag the service Nginx :80 with front
- Request Attribute => to catch the parameter **LSN**, **LTN**, **SI**, **TSN**, **VU** which are contain in the http header : x-dynatrace-test : VU=1;TSN=Login;SI=JMeter;LSN=KeyTransactions;LTN=DT_Training;...  
- Request Naming : **{RequestAttribute:SI} {RequestAttribute:TSN}**

1) download monaco

       cd;cd ace-load-testing-automation;
       wget https://github.com/dynatrace-oss/dynatrace-monitoring-as-code/releases/download/v1.5.2/monaco-linux-amd64;
       mv monaco-linux-amd64 monaco;
       chmod +x monaco;
       export NEW_CLI=1;
       ./monaco --version

2) create your token   
Go to your Dynatrace environment :  _Settings > Integration > Dynatrace API > Generate Token_   
With these privileges (more info about token permission for monaco [here](https://github.com/dynatrace-oss/dynatrace-monitoring-as-code#supported-configuration-types-and-token-permissions):  
    <img src="https://user-images.githubusercontent.com/40337213/115966397-aed15d80-a52d-11eb-8156-a278b8f9a489.png" width="700" height="250">

       tip: keep the value of the token you will not be able to display it afterwards 

3) export your environment variables for monaco 
export tenant abcd123.live.dynatrace.com variable without https://

       export MyTenant=abcd123.live.dynatrace.com
       export MyToken=xxxx1234yyyy1234
       

4) deploy the configuration for dynatrace with monaco 

- deploy tag and request attribute  
       
      cd;cd easy-loadtesting-integration;
      ./monaco deploy -e=environments.yaml 01-deploy-config-with-Monaco/step1

- deploy request naming

      cd;cd easy-loadtesting-integration;
      ./monaco deploy -e=environments.yaml 01-deploy-config-with-Monaco/step2

5) validate the imported configuration in Dynatrace with monaco  
- tag=**front** : you must have the Nginx Service.  
  The integration with Jmeter and Dynatrace is done thanks this **tag=front** on the front web serveur service. 
![image](https://user-images.githubusercontent.com/40337213/116276454-d79f6000-a784-11eb-96a0-d9753d841487.png)

- Request Attribute: LSN, LTN, SI, TSN, VU  
![image](https://user-images.githubusercontent.com/40337213/116272650-61e5c500-a781-11eb-967f-cd3501b21927.png)
**VU** = Virtual User ID of the unique user who sent the request.  
**SI** = Source ID identifies the product that triggered the request (JMeter, LoadRunner, Neotys, or other).  
**TSN** = Test Step Name is a logical test step within your load testing script (for example, Login or Add to cart).  
**LSN** = Load Script Name - name of the load testing script. This groups a set of test steps that make up a multistep transaction (for example, an online purchase).  
**LTN** = The Load Test Name uniquely identifies a test execution (for example, 6h Load Test – June 25).  
**PC** = Page Context provides information about the document that is loaded in the currently processed page.  

- Request Naming : {RequestAttribute:SI} {RequestAttribute:TSN}
![image](https://user-images.githubusercontent.com/40337213/116273665-40d1a400-a782-11eb-841f-43507a8cc2a6.png)

4) troubleshoot for monaco step  

| Step  | test |Status |
| --------------- | --------------- | --------------- | 
| export NEW_CLI=1 | echo "NEW_CLI="$NEW_CLI  | ✔️ |
| export MyTenant=1234.live.dynatrace.com | echo "MyTenant=https://"$MyTenant  | ✔️ |
| export MyToken=abcd1234xyz| echo "MyToken="$MyToken | ✔️ |
| cd;git clone https://github.comdynatrace-ace-services/easy-loadtesting-integration | cd;ls -lrt dynatrace-ace-services | ✔️ |
| monaco installed with NEW_CLI=1 (new monaco cli version) | cd;cd monaco-lab;./monaco --version  | ✔️ |

# Next Step
- [02-loadtesting-Integration](https://github.com/dynatrace-ace-services/easy-loadtesting-integration/tree/main/02-loadtesting-Integration) => to run the load test with Dynatrace integration

