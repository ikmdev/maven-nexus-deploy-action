# Title

This runs after a successful build. It is responsible for publishing artifacts to [Nexus](https://nexus.tinkarbuild.com).

### Team Ownership - Product Owner

Automation Team

## How to Use

This workflow is automatically triggered after a successful build located in the `.github/workflows` folder, as described in the 
[GitHub Documentation](https://docs.github.com/en/actions/writing-workflows/quickstart).  

```yaml
jobs:
  publish-artifacts:
      name: Publish Artifacts
      runs-on: ubuntu-24.04
      if: github.event.workflow_run.conclusion == 'success' && github.repository_owner == 'ikmdev'
      steps:
      - uses: actions/setup-java@v4
        with:
                java-version: '21'
                distribution: 'zulu'


      - name: Deploy Artifacts To Nexus
        uses: ikmdev/maven-nexus-deploy-action@main
        with:
            nexus_repo_password: ${{secrets.EC2_NEXUS_PASSWORD}}
            repo_name: ${{github.event.workflow_run.head_repository.full_name}}
            branch_name: ${{github.event.workflow_run.head_branch}}
```

## Issues and Contributions
Technical and non-technical issues can be reported to the [Issue Tracker](https://github.com/ikmdev/maven-nexus-deploy-action/issues).

Contributions can be submitted via pull requests. Please check the [contribution guide](doc/how-to-contribute.md) for more details.
