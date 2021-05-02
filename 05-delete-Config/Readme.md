# 05-delete-Config

1) validate your env variables 

       echo "NEW_CLI="$NEW_CLI;echo "MyTenant=https://"$MyTenant;echo "MyToken="$MyToken;echo "Appname="$Appname;
  
2) delete your configuration  
 Don't worry, it will delete only the configuration from monaco_lab and not your others Dynatrace configurations ;)

       cd;cd ace-load-testing-automation;
       ../monaco deploy -e=environments.yaml -delete-Config
       
 # In summary 
it's what you can import in your Jenkins to automate your monitoring 
      
- export the variables

      export NEW_CLI=1;
      export MyTenant=https://abcd.live.dynatrace.com
      export MyToken=ABCD123456XYZ
      export Appname=<Host_Group>
      export Hostname=<myhostname.domaine.com>

- update the config

      cd;
      cd ace-load-testing-automation;
      git pull;
      cp test-plan-* ../docker-jmeter/tests/
       

- deploy the config

      cd;
      cd ace-load-testing-automation;
      ./monaco deploy -e=environments.yaml 01-deploy-config-with-Monaco/step1;
      ./monaco deploy -e=environments.yaml 01-deploy-config-with-Monaco/step2;
      ./monaco deploy -e=environments.yaml 04-driven-Slo/Metric;
      ./monaco deploy -e=environments.yaml 04-driven-Slo/Slo;
      cd;
      cd docker-jmeter;
      ./run.sh  -n -t tests/test-plan-with-integration.jmx -Jtenant=$MyTenant -Jtoken=$MyToken -Jhostname=$Hostname -l tests/loadest.jlt
  
 # Next Step
- [06-next-Step](https://github.com/ace-dynatrace-lab/ace-load-testing-automation/tree/main/06-next-Step) => now you are ready to integrate Dynatrace configuration to your CICD pipeline.

  
