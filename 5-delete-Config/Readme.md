# 4-delete-Config

1) validate your env variables 

       echo "NEW_CLI="$NEW_CLI;echo "MyTenant=https://"$MyTenant;echo "MyToken="$MyToken;echo "Appname="$Appname;
  
2) delete your configuration  
 Don't worry, it will delete only the configuration from monaco_lab and not your others Dynatrace configurations ;)

       cd;cd load-testing-automation;
       ../monaco deploy -e=environments.yaml -delete-Config
       
  # Next Step
- [06-next-Step](https://github.com/dynatracelab/load-testing-automation/tree/main/06-next-Step) => now you are ready to integrate Dynatrace configuration to your CICD pipeline.

  
