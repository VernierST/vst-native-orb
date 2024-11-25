# vst-native-orb

Most of the steps are the same for building all the native code since conan is used.
This orb contains the common commands, executors, and jobs.

## Setup CI on a vst native projects

1. Go to the CircleCI project dashboard. [
BitBucket](https://app.circleci.com/projects/project-dashboard/bitbucket/vernierst/) or [Github](https://app.circleci.com/projects/project-dashboard/github/VernierST/)
2. Select the `Set Up Project` for the project.
3. Select the `Use Existing` and then `Start Building` so that it doesn't add a config.yml. *Note:* The build will fail and that is fine.
4. Select the `Project Settings` and then `Environment Variables`. Now select `Import Variables` and select `libvstudm` and then `Import Variables`. This is going to import the gitlab keys used for publishing.
5. Now select `SSH Keys` because we need to access *vst-setup-conan* repo the deploy will not work. We need to seled `Add User Key`, if you are on Bitbucket make sure you [See the Bitbucket integration docs before you add the key](https://circleci.com/docs/2.0/gh-bb-integration/#creating-a-bitbucket-user-key).
6. Once you have the `sha` you will need to add it to the `sdk` access keys and `vst-conan-setup` access keys. The `fingerprint` for the user key will need to be set in the params of the config.yml, see below for details.



## Example .circleci/config.yml using vst-native-orb

```
version: 2.1

orbs:
  vst: vst/vst-native-orb@1.0.0

.current_filters: &current_filters
  branches:
    only:
      - main
      - /^pr-ci\/.+/

.params: &params
  package-name: "libxml2"
  install-cmake: false
  install-autotools: true
  vcs-fingerprint: "00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00"
  build-missing: false

workflows:
  version: 2
  build:
    jobs:
      - vst/mac_build:
          <<: *params
          filters:
            <<: *current_filters
      - vst/win_build:
          <<: *params
          filters:
            <<: *current_filters
      - vst/linux_build:
          <<: *params
          filters:
            <<: *current_filters
```

**Most of the sdk config.yml will only differ with the params**

* **package-name**
    Name that needs to match the conan files
* **install-cmake**
    True if CMake needs to be installed
* **install-autotools**
    True if autotools need to be installed
* **vcs-fingerprint**
    CircleCI fingerprint assigned to the user key, this is used to setup ssh so that CI can access the source repositories
* **build-missing**
    Defaulted to false so we fail when a dependency hasn't already built and deployed but sometimes you might just want to let conan build it.
## See:
 - [Orb Author Intro](https://circleci.com/docs/2.0/orb-author-intro/#section=configuration)
 - [Reusable Configuration](https://circleci.com/docs/2.0/reusing-config)