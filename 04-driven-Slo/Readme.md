# 04-driven-Slo

In this steb, we will import a SLO to mesure the objectif of having at least 95% of SpecialOffers requests under 500 milisecondes.  
<img src="https://user-images.githubusercontent.com/40337213/116290032-54d1d180-a793-11eb-8bf7-adb8c18bb42d.png" width="400" height="700">


1) import slo configuration with monaco
You need to add **Read SLO** and **Write SLO** from API V2 privilege to your token. 

- Import the metric

      cd;cd ace-load-testing-automation;
      ./monaco deploy -e=environments.yaml 04-driven-Slo/Metric;

- Import the Slo

      cd;cd ace-load-testing-automation;
      ./monaco deploy -e=environments.yaml 04-driven-Slo/Slo;

2) run a new loat test

       cd; cd docker-jmeter;
       ./run.sh  -n -t tests/test-plan-with-integration.jmx -Jtenant=$MyTenant -Jtoken=$MyToken -Jhostname=$Hostname -l tests/loadest.jlt

3) valiate the result

![image](https://user-images.githubusercontent.com/40337213/116288031-5ef2d080-a791-11eb-9b51-084130a39f7c.png)


  # Next Step
- [05-delete-Config](https://github.com/ace-dynatrace-lab/ace-load-testing-automation/tree/main/05-delete-Config) => to clean the environment
