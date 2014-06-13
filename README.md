This example is in response to the question on Salesforce StackExchange [How can I deploy and remove components in one step with the ant migration tool?](http://salesforce.stackexchange.com/questions/40398/how-can-i-deploy-and-remove-components-in-one-step-with-the-ant-migration-tool). Metadata component additions and updates should be included in the `package.xml`, component removals should be included in `destructiveChanges.xml`.

##Instructions
1. Configure your `<USERNAME>` and `<PASSWORD>` in the `build.properties`
2. Deploy the `initial-package`, this just deploys 2 Apex classes, one to be updated and the other to be deleted:
  ```
  $> ant deploy-initial-package
  Buildfile: /home/alan/sf-ant-test/build.xml
  
  deploy-initial-package:
  [sf:deploy] Request for a deploy submitted successfully.
  [sf:deploy] Request Id for the current deploy task: 09Sf0000001BfvdEAC
  [sf:deploy] Waiting for server to finish processing the request...
  [sf:deploy] Request Status: InProgress
  [sf:deploy] Request Status: InProgress
  [sf:deploy] Request Status: Completed
  [sf:deploy] Finished request 09Sf0000001BfvdEAC successfully.

  BUILD SUCCESSFUL
  Total time: 1 minute 33 seconds
  ```
3. Verify `AntTest_Updated.cls` and `AntTest_ToBeRemoved.cls` now exist in your Org.
4. Deploy the `add-update-delete-package`:
  ```
  $> ant deploy
  Buildfile: /home/alan/sf-ant-test/build.xml

  deploy:
  [sf:deploy] Request for a deploy submitted successfully.
  [sf:deploy] Request Id for the current deploy task: 09Sf0000001Bg17EAC
  [sf:deploy] Waiting for server to finish processing the request...
  [sf:deploy] Request Status: InProgress
  [sf:deploy] Request Status: InProgress
  [sf:deploy] Request Status: Completed
  [sf:deploy] Finished request 09Sf0000001Bg17EAC successfully.

  BUILD SUCCESSFUL
  Total time: 1 minute 34 seconds
  ```
5. Verify the results:
  - `AntTest_Added` should now exist
  - `AntTest_Updated` should have a method called `newMethod` added.
  - `AntTest_ToBeRemoved` should no longer exist
