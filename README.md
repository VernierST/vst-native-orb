# Orb Project Template

[![CircleCI Orb Version](https://img.shields.io/badge/endpoint.svg?url=https://badges.circleci.io/orb/vst/vst-native-orb)](https://circleci.com/orbs/registry/orb/vst/vst-native-orb) [![GitHub License](https://img.shields.io/badge/license-MIT-lightgrey.svg)](https://raw.githubusercontent.com/VernierST/vst-native-orb/main/LICENSE) [![CircleCI Community](https://img.shields.io/badge/community-CircleCI%20Discuss-343434.svg)](https://discuss.circleci.com/c/ecosystem/orbs)


Additional READMEs are available in each directory.


## Resources

[CircleCI Orb Registry Page](https://circleci.com/orbs/registry/orb/vst/) - The official registry page of this orb for all versions, executors, commands, and jobs described.
[CircleCI Orb Docs](https://circleci.com/docs/2.0/orb-intro/#section=configuration) - Docs for using and creating CircleCI Orbs.

### How to Contribute

We welcome [issues](https://github.com/VernierST/vst-native-orb/issues) to and [pull requests](https://github.com/VernierST/vst-native-orb/pulls) against this repository!

### How to Publish
* Create and push a branch with your new features.
* When ready to publish a new production version, create a Pull Request from _feature branch_ to `main`.
* The title of the pull request must contain a special semver tag: `[semver:<segement>]` where `<segment>` is replaced by one of the following values.

| Increment | Description|
| ----------| -----------|
| major     | Issue a 1.0.0 incremented release|
| minor     | Issue a x.1.0 incremented release|
| patch     | Issue a x.x.1 incremented release|
| skip      | Do not issue a release|

Example: `[semver:major]`

* Squash and merge. Ensure the semver tag is preserved and entered as a part of the commit message.
* On merge, after manual approval, the orb will automatically be published to the Orb Registry.

Please keep the orb major version the same as the major version of the
conan config package it uses.

For further questions/comments about this or other orbs, visit the Orb Category of [CircleCI Discuss](https://discuss.circleci.com/c/orbs).

NOTE: if the orb update triggers 'The dev version of vst/vst-native-orb@dev:alpha has expired. Dev versions of orbs are only valid for 90 days after publishing.', the dev orb needs to be re-published:

  circleci orb pack src > dist/orb.yml
  circleci orb validate dist/orb.yml
  circleci orb publish dist/orb.yml vst/vst-native-orb@dev:alpha

After that touch the main repo again to trigger the CI pipeline
