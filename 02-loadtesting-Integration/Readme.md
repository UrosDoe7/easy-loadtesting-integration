# 2-loadtest-with-dynatrace-integration

In this step we will run the load test on a test plan with Dynatrace integartion   

1) test-plan-with-integration : find the jmx [here](https://github.com/ace-dynatrace-lab/ace-load-testing-automation/blob/main/test-plan-with-integration.jmx) 
Short description of the run load test for integration :  
- [event-checking](https://github.com/ace-dynatrace-lab/ace-load-testing-automation/blob/main/2-loadtest-with-dynatrace-integration/event-checking.json)
![image](https://user-images.githubusercontent.com/40337213/116277404-bab75c80-a785-11eb-8caf-dfcee8e498e4.png)

- **Login** with x-dynatrace-test
![image](https://user-images.githubusercontent.com/40337213/116277534-dd497580-a785-11eb-8ef1-d18913dd83a9.png)

- **Search** with x-dynatrace-test
![image](https://user-images.githubusercontent.com/40337213/116277666-feaa6180-a785-11eb-9e35-f707f06d910e.png)

- **Special offer** with x-dynatrace-test
![image](https://user-images.githubusercontent.com/40337213/116277790-1aae0300-a786-11eb-80d5-80a797c41323.png)

- [event-checkout](https://github.com/ace-dynatrace-lab/ace-load-testing-automation/blob/main/2-loadtest-with-dynatrace-integration/event-checkout.json)  
![image](https://user-images.githubusercontent.com/40337213/116277935-4335fd00-a786-11eb-9db9-90261e9a33ea.png)

- [annotation-checkout](https://github.com/ace-dynatrace-lab/ace-load-testing-automation/blob/main/2-loadtest-with-dynatrace-integration/event-checkout.json), between start and stop    
![image](https://user-images.githubusercontent.com/40337213/116278174-88f2c580-a786-11eb-865d-c1ad5a258157.png)


2) run the load test with integration   

       cd; cd docker-jmeter;
       ./run.sh  -n -t tests/test-plan-with-integration.jmx -Jtenant=$MyTenant -Jtoken=$MyToken -Jhostname=$Hostname -l tests/loadest.jlt
       
 - the result when everything works            
![image](https://user-images.githubusercontent.com/40337213/116279645-12ef5e00-a788-11eb-9c12-0149e1c3f234.png)

3) troubleshoot    

- variables
 
       echo "MyTenant=https://"$MyTenant" ===> "` curl -Is https://$MyTenant | head -n 1`;echo "MyToken="$MyToken;echo "Hostname="$Hostname" ===> "` curl -Is http://$Hostname | head -n 1;
       
- jmeter
       
      cd;cd docker-jmeter;
      ./run.sh  -n -t tests/test-plan-with-integration.jmx -Jtenant=$MyTenant -Jtoken=$MyToken -Jhostname=$Hostname -L DEBUG -l tests/loadest.jlt &
      tail -f tests/LoadTest.jl                 
                 
# Next Step
- [03-results-in-Dynatrace](https://github.com/ace-dynatrace-lab/ace-load-testing-automation/tree/main/03-results-in-Dynatrace) => to analyse the result in Dynatrace
