# Build Arch Linux Package

Build Arch Linux package with GitHub Actions.

See [action.yml](action.yml) for usage. The meaning of inputs and outputs are written in the description.


```
---
name: Build package
on: [push]
jobs:
  Build-package:
    runs-on: ubuntu-latest
    container:
      image: manjarolinux/base
      options: --privileged
    name: Build of ${{ matrix.platform }}
    strategy:
        fail-fast: false
        matrix:
#          platform: [ 'x86_64' ]
          platform: [ 'x86_64', 'aarch64' ]
    steps:
      - uses: jmlich/nemo-package@master
        with:
          platform: ${{ matrix.platform }}
          pkg_builds_repo: nemomobile-ux/nemo-packaging
          pkg_build_path: lipstick-glacier-home-git
#          pacman_branch: unstable
          overlay_repo_url: https://nemo.mlich.cz/build-results-${{ matrix.platform }}/packages/
          overlay_repo_name: nemomobile
          extra_packages: qt5-quickcontrols-nemo-git qt5-glacier-app-git
```