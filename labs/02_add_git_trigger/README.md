# Adding GitHub Triggers

This folder holds the files for the lab: _Adding GitHub Triggers_ which is part of the **IBM-CD0215EN-Skills Network Introduction to CI/CD** course.


# To Test 
You need terminals to test how it works 
## Terminal 1
In one of the sessions, you need to run the kubectl port-forward command to forward the port for the event listener so that you can call it on localhost.

Use the kubectl port-forward command to forward port 8090 to 8080. Run the following command
```
$ kubectl port-forward service/el-cd-listener  8090:8080
```
You will see the following output, but you will not get your cursor back.
```
$ Forwarding from 127.0.0.1:8090 -> 8080
$ Forwarding from [::1]:8090 -> 8080
```

## Terminal 2
Now you are ready to trigger the event listener by posting to the endpoint that it is listening on. You will now need to open a second terminal shell to issue commands.

Open a new Terminal shell wtih the menu item Terminal > New Terminal.

Use the curl command to send a payload to the event listener service.

```
curl -X POST http://localhost:8090 \
  -H 'Content-Type: application/json' \
  -d '{"ref":"main","repository":{"url":"https://github.com/LegendaryPark/wtecc-CICD_PracticeCode.git"}}'
```

You can also examine the PipelineRun logs using this command (the -L means “latest” so that you do not have to look up the name for the last run):

```
tkn pipelinerun logs --last
```