# 00-start-with-Jmeter

In this lab you will install a Jmeter docker on your linux host. 

1) install jmeter 

       cd;
       git clone https://github.com/justb4/docker-jmeter.git;
       ./build.sh
       
- try it for help 

      cd;
      cd docker-jmeter/;
      ./run.sh --?
       
4) download this lab  

       cd;
       git clone https://github.com/dynatrace-ace-services/easy-loadtesting-integration

5) copy the tests plan  

       cd;
       cp easy-loadtesting-integration/test-plan-* docker-jmeter/tests/

2) export your fisrt environment variable  

       export Hostname=<myhostname.domaine.com> (without https://...)

- verify your env variable  

       echo "Hostname="$Hostname" ===> "` curl -Is http://$Hostname | head -n 1`
       
6) start the jmeter scenario without dynatrace integration 
       
       cd;cd docker-jmeter;
       ./run.sh -n -t tests/test-plan-without-integration.jmx -Jhostname=$Hostname -l tests/loadtest.jlt

   ![image](https://user-images.githubusercontent.com/40337213/116146424-c69c1380-a6de-11eb-82a9-884c7afe7d0f.png)
   ![image](https://user-images.githubusercontent.com/40337213/116276203-973fe200-a784-11eb-9b70-921f53ea8ea3.png)


7) test-plan-without-integration : find the jmx [here](https://github.com/dynatrace-ace-services/easy-loadtesting-integration![image](https://user-images.githubusercontent.com/40337213/118807550-be339480-b8a8-11eb-828f-59fdea43da82.png)
/blob/main/test-plan-without-integration.jmx)   
Short description of the test plan without dynatrace integration:  
- Load Test Step: **Login**
![image](https://user-images.githubusercontent.com/40337213/116147594-3a8aeb80-a6e0-11eb-8a70-21c345d6b4c3.png)
- Load Test Step: **Search**
![image](https://user-images.githubusercontent.com/40337213/116147754-627a4f00-a6e0-11eb-9a10-29886fdd761b.png)
- Load Test Step: **SpecialOffer**
![image](https://user-images.githubusercontent.com/40337213/116147815-745bf200-a6e0-11eb-8fac-be560efcf8d7.png)

8) (optional) if you want to open the test plan, install jmeter on your own laptop clic [here](https://jmeter.apache.org/download_jmeter.cgi)  
  Follow the workflow :  
         <img src="https://user-images.githubusercontent.com/40337213/116146851-44f8b580-a6df-11eb-852e-1fbc541227f9.png" width="400" height="100">


9) troubleshoot  

| Step  | test |Status |
| --------------- | --------------- | --------------- | 
| export Hostname=<myhostname.domain.com> |echo "Hostname="$Hostname  | ✔️ |
| OneAgent installed with hostgroup=appname | service oneagent status | ✔️ |
| cd;git clone https://github.com/justb4/docker-jmeter.git | ls docker-jmeter | ✔️ |
| cd;git clone https://github.com/dynatrace-ace-services/easy-loadtesting-integration | ls easy-loadtesting-integration | ✔️ |
| cd;mv easy-loadtesting-integration/test-plan-with* docker-jmeter/tests/ | ls docker-jmeter/tests | ✔️ |
| easytravel installed and started (accessible from your browser) | curl -Is http://$Hostname | ✔️ |
| loadgen is stopped | docker-compose stop loadgen | ✔️ |
| cd;cd /docker-jmeter;./run.sh -n -t tests/easy-loadtesting-integration/test-plan-without-integration.jmx -Jhostname=$Hostname -l tests/loadtcd esting-lab/LoadTest.jlt & | tail -f ests/loadtcd esting-lab/LoadTest.jlt | ✔️ |

# Next Step  

- [01-deploy-config-with-Monaco](https://github.com/dynatrace-ace-services/easy-loadtesting-integration/tree/main/01-deploy-config-with-Monaco) => to prepare the environment with request attribute, etc..
