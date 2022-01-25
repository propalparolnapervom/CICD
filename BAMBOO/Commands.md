## Variables

[Variables](https://confluence.atlassian.com/bamboo/bamboo-variables-289277087.html)

Some of the pre-defined variables that can be used within Bamboo tasks, for example
```
echo "bamboo.buildKey: ${bamboo.buildKey}"
echo "bamboo.planKey: ${bamboo.planKey}"
echo "bamboo.shortPlanKey: ${bamboo.shortPlanKey}"
echo "bamboo.shortJobKey: ${bamboo.shortJobKey}"
echo "bamboo.buildResultKey: ${bamboo.buildResultKey}"
echo "bamboo.buildResultsUrl: ${bamboo.buildResultsUrl}"
echo "bamboo.resultsUrl: ${bamboo.resultsUrl}"
echo "bamboo.buildNumber: ${bamboo.buildNumber}"
echo "bamboo.buildPlanName: ${bamboo.buildPlanName}"
echo "bamboo.shortPlanName: ${bamboo.shortPlanName}"
echo "bamboo.shortJobName: ${bamboo.shortJobName}"
echo "bamboo.buildTimeStamp: ${bamboo.buildTimeStamp}"
echo "bamboo.agentId: ${bamboo.agentId}"
echo "bamboo.agentWorkingDirectory: ${bamboo.agentWorkingDirectory}"
echo "bamboo.build.working.directory: ${bamboo.build.working.directory}"
echo "bamboo.ManualBuildTriggerReason.userName: ${bamboo.ManualBuildTriggerReason.userName}"
echo "bamboo.repository.pr.key: ${bamboo.repository.pr.key}"
echo "bamboo.repository.pr.sourceBranch: ${bamboo.repository.pr.sourceBranch}"
echo "bamboo.repository.pr.targetBranch: ${bamboo.repository.pr.targetBranch}"
echo "bamboo.planRepository.branchDisplayName: ${bamboo.planRepository.branchDisplayName}"
```
