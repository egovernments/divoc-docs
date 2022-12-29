# Configuring Environment Variables in 2.0

Environment variables are added in divoc-config.yml in the orchestration node.

### Steps to add the environment variables:

* To display the config map, run the following command:

```
kubectl -n divoc get configmap 
```

* If multiple config maps exist, add environment variables to all the config maps.
* To edit the config map, run the following command:&#x20;

```
kubectl -n divoc edit config divoc-config
```

* Next, add the variables under ‘data.’ Save and exit.
* Restart the services where environment variables have been used by running the following command:&#x20;

```
kubectl -n divoc rollout restart <service_name>
```



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
