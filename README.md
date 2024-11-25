### How to Publish An Update
1. Merge pull requests with desired changes to the main branch.
2. Find the current version of the orb.
    - You can run `circleci orb info vst/vst-frontend-orb | grep "Latest"` to see the current version.
3. Tag main with a semantic version tag, e.g., v1.0.1 (the 'v' prefix is mandatory)
4. Push tag to repository, this triggers CircleCI build of the orb
5. Check on CircleCI the build succeeded

### Development versions of the orb

Prerequisites: cicleci CLI install and configured

1. Make your local changes
2. Pack the the orb:
    `circleci orb pack src/ > dist/orb.yml`
3. Validate the orb:
    `circleci orb validate dist/orb.yml`
4. Publish a dev version, assuming validation passed:
    `circleci orb publish dist/orb.yml vst/vst-frontend-orb@dev:1.0.1
5. Use the 'dev:1.0.1' version to build a draft PR.

NOTE: if the orb update triggers 'The dev version of vst/vst-native-orb@dev:alpha has expired. Dev versions of orbs are only valid for 90 days after publishing.', the dev orb needs to be re-published:

  circleci orb pack src > dist/orb.yml
  circleci orb validate dist/orb.yml
  circleci orb publish dist/orb.yml vst/vst-native-orb@dev:alpha

After that touch the main repo again to trigger the CI pipeline
