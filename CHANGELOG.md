# Changelog

All notable changes to this project will be documented in this file.

This project adheres to [Semantic Versioning](https://semver.org/).


## 1.1.1

Previously: `1.0.0-dev` **(+)** `Dev_prerelease` -> `1.0.1-dev1`  
Now: `1.0.0-dev` **(+)** `Dev_prerelease` -> `1.0.0-dev1`  

> Unchanged behaviour when "current sem ver" does not contain pre release metadata
> `1.0.0` **(+)** `Dev_prerelease` -> `1.0.1-dev`

### Changes

#### Fix

- Refactored DEV_PRERELEASE operator to only increment patch when the current version is not already a dev release.


## 1.1.0

### Changes

#### Feature

- Add case-insensitive support for bump operators. Now accepts both uppercase (e.g., 'MAJOR') and lowercase (e.g., 'major') variants.


## 1.0.1

This Release started with adding **Automated Test Cases** for `bumping` Sem Vers below (stable) 1.0.0 version. 

In the process, apart from CI improvements, a **bug was fixed**, where the `Dev PreRelease` operator was missing instructions to **add +1** on the `patch` of the sem ver.

### Changes

#### Fix
- increment patch by 1 for `Dev PreRelease` operator (#9553855)

#### Test
- add Test Case for `Dev PreRelease` bump on `0.41.0` SemVer (#6d3ff24)
- add 2 Test Cases for version `0.41.0` (#33b2fb6)

#### CI
- fix Bash syntax in CD pipeline (#bdf2f2d)
- change `Dev PreRelease` tests output expectations (#7518089)
- remove unused Job step (#55d9a34)

#### Docs
- fix syntax in `README.md` (#b7dce48)


## 1.0.0

`First Stable Release`, with **9 Test Cases** and **CI/CD Pipeline**.

### Changes

#### Fix
- corrent Github Expression syntax, when checking for supported `input Bump`
- proper Bash Env Vars value assignment

#### Test
- 9 Test Cases utilizing all Version Bump Levels and runtime vs expected assertion

#### Docs
- enlist notable `features` of the Sem Ver Bumper Action, in `README.md`

#### CI
- add CI/CD Pipeline with Automated Test Matrix populated with Test Cases


## 0.1.0

This is the **first** ever release of the **Action Sem Ver Bumper** Open-Source Project.
- The project is hosted in a public repository on GitHub at [https://github.com/boromir674/action-semver-bumper](https://github.com/boromir674/action-semver-bumper)

### Initial Sources

- **CI/CD Pipeline** running on GitHub Actions at [https://github.com/boromir674/action-semver-bumper/actions](https://github.com/boromir674/action-semver-bumper)
