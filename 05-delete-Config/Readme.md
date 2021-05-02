# 05-delete-Config

1) validate your env variables 

       echo "NEW_CLI="$NEW_CLI;echo "MyTenant=https://"$MyTenant;echo "MyToken="$MyToken;echo "Appname="$Appname;
  
2) delete your configuration  
 Don't worry, it will delete only the configuration from monaco_lab and not your others Dynatrace configurations ;)

       cd;cd ace-load-testing-automation;
       ../monaco deploy -e=environments.yaml -delete-Config
       

# Next Step
- [06-in-Summary](https://github.com/ace-dynatrace-lab/ace-load-testing-automation/tree/main/06-in-Summary) => it's an overview of the task you can easily automate.
