# Semantic Version Bumper

> Bump a Semantic Version based on a given operator.

[![GitHub Actions Workflow Status - cicd.yml](https://img.shields.io/github/actions/workflow/status/boromir674/action-semver-bumper/cicd.yml?label=CI%2FCD)](https://github.com/boromir674/action-semver-bumper/actions/workflows/cicd.yml)
![GitHub Tag](https://img.shields.io/github/v/tag/boromir674/action-semver-bumper?sort=semver)
![GitHub Release](https://img.shields.io/github/v/release/boromir674/action-semver-bumper?sort=semver&color=blue)
![GitHub commits since latest release (by SemVer)](https://img.shields.io/github/commits-since/boromir674/action-semver-bumper/latest?color=blue&logo=semver&sort=semver)
[![License](https://img.shields.io/github/license/boromir674/action-semver-bumper)](https://github.com/boromir674/action-semver-bumper/blob/main/LICENSE)


```mermaid

graph LR

%% INPUT INFORMATION

INPUT_SEM_VER(("`Current **Sem Ver**`"))
INPUT_SEM_VER_BUMP_OPERATOR(("`Sem Ver **Bump Operator**`"))


%% CONDITION NODES

COND_SEM_VER_BUMP_OPERATOR{"`Bump Operator Function`"}


%% SEM VER BUMP OPERATION

SEM_VER_INCREMENT_MAJOR["`Set **MAJOR** +=1
set **Minor** = 0
set **patch** = 0`"]
SEM_VER_INCREMENT_MINOR["`Set **Minor** += 1
set **patch** = 0`"]
SEM_VER_INCREMENT_PATCH["`Set **patch** += 1`"]
SEM_VER_INCREMENT_PATCH_N_ADD_PRERELEASE_METADATA["`Set **patch** += 1
append '-dev'`"]

%%%% GRAPH DESIGN %%%%

INPUT_SEM_VER_BUMP_OPERATOR -.-> COND_SEM_VER_BUMP_OPERATOR



%% COND_SEM_VER_BUMP_OPERATOR --MAJOR --> COND_STABLE_ALREADY_RELEASED

%% COND_STABLE_ALREADY_RELEASED --No --> SEM_VER_SET_TO_1_0_0
%% COND_STABLE_ALREADY_RELEASED --Yes --> SEM_VER_INCREMENT_MAJOR

%% INPUT_SEM_VER -...-> SEM_VER_INCREMENT_MAJOR
%% INPUT_SEM_VER -...-> SEM_VER_INCREMENT_MINOR
%% INPUT_SEM_VER -...-> SEM_VER_INCREMENT_PATCH
%% INPUT_SEM_VER -...-> SEM_VER_INCREMENT_PATCH_N_ADD_PRERELEASE_METADATA


COND_SEM_VER_BUMP_OPERATOR --MAJOR --> SEM_VER_INCREMENT_MAJOR
COND_SEM_VER_BUMP_OPERATOR --Minor --> SEM_VER_INCREMENT_MINOR
COND_SEM_VER_BUMP_OPERATOR --patch --> SEM_VER_INCREMENT_PATCH
COND_SEM_VER_BUMP_OPERATOR --dev prerelease --> SEM_VER_INCREMENT_PATCH_N_ADD_PRERELEASE_METADATA


%% APPLY_OPERATOR(("`Current Version + Operator = New Sem Ver`"))
%% INPUT_SEM_VER -..-> APPLY_OPERATOR(("`Current Version + Operator = New 
%% Sem Ver`"))

%% APPLY_OPERATOR("`Apply Operator on
%% Current Version`")

INPUT_SEM_VER -...-> APPLY_OPERATOR
APPLY_OPERATOR(("`'+'`"))

%% CONNECT ALL BUMPS to OPERATOR
SEM_VER_INCREMENT_MAJOR --> APPLY_OPERATOR
SEM_VER_INCREMENT_MINOR --> APPLY_OPERATOR
SEM_VER_INCREMENT_PATCH --> APPLY_OPERATOR
SEM_VER_INCREMENT_PATCH_N_ADD_PRERELEASE_METADATA --> APPLY_OPERATOR

%% INPUT_SEM_VER --> NEW_SEM_VER(("`New SEM VER`"))
APPLY_OPERATOR --> NEW_SEM_VER(("`New **SEM VER**`"))

```


## Inputs

| Input           | Description                                                                 | Required | Default |
|-----------------|-----------------------------------------------------------------------------|----------|---------|
| `sem_ver`       | The current Semantic Version.                                               | `true`   |         |
| `bump_operator` | The bump operator to apply. Valid values are `MAJOR`, `MINOR`, `PATCH`, `DEV_PRERELEASE`. | `true`   |         |

## Outputs

| Output         | Description                                |
|----------------|--------------------------------------------|
| `new_sem_ver`  | The new Semantic Version after applying the bump operator. |

## Usage

```yaml
name: Bump Semantic Version
on: [push]

jobs:
  bump_version:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Bump Semantic Version
        id: bump_version
        uses: boromir674/action-semver-bumper@v1.0.0
        with:
          sem_ver: '1.0.0'
          bump_operator: 'MINOR'

      - name: Get the new version
        run: echo "New Semantic Version is ${{ steps.bump_version.outputs.new_sem_ver }}"
```

### Example

#### Bumping MAJOR Version

```yaml
- name: Bump Major Version
  id: bump_major
  uses: boromir674/action-semver-bumper@v1.0.0
  with:
    sem_ver: '1.0.0'
    bump_operator: 'MAJOR'
```

#### Bumping Minor Version

```yaml
- name: Bump Minor Version
  id: bump_minor
  uses: boromir674/action-semver-bumper@v1.0.0
  with:
    sem_ver: '1.0.0'
    bump_operator: 'MINOR'
```

#### Bumping Patch Version

```yaml
- name: Bump Patch Version
  id: bump_patch
  uses: boromir674/action-semver-bumper@v1.0.0
  with:
    sem_ver: '1.0.0'
    bump_operator: 'PATCH'
```

#### Bumping with Prerelease Metadata

```yaml
- name: Bump with Dev Prerelease
  id: bump_dev_prerelease
  uses: boromir674/action-semver-bumper@v1.0.0
  with:
    sem_ver: '1.0.0'
    bump_operator: 'DEV_PRERELEASE'
```
