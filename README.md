# Arduino-CI GitHub Action

This repository is for the **GitHub Action** to run [`arduino_ci`](https://github.com/Arduino-CI/arduino_ci) on a repository containing an Arduino library.

## Why You Should Use This Action

- Contributions to your Arduino library are tested automatically, _without_ the need for hardware present
- Example sketches in your `examples/` directory are compiled automatically, to detect broken code in the default branch


## Adding Arduino CI To Your Project

1. Create a new YAML file in your repository's `.github/workflows` directory, e.g. `.github/workflows/arduino_test_runner.yml`
2. Copy an example workflow from below into that new file, no extra configuration required
3. Commit that file to a new branch
4. Open up a pull request and observe the action working
5. Merge into your default branch to enable testing of all following pull requests


### Configuring a Wokflow to Use the GitHub Action

These contents for `.github/workflows/arduino_test_runner.yml` should work for most people.

```yml
---
name: Arduino CI

on: [pull_request]

jobs:
  arduino_ci:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - uses: Arduino-CI/action@v0.1.0
        env:
          # Not all libraries include examples or unit tests.  The default
          #  behavior of arduino_ci is to assume that "if the files don't
          #  exist, then they were not MEANT to exist".  In other words,
          #  if you were to accidentally delete all your tests or example
          #  sketches, then the CI runner would by default assume that was
          #  intended and return a passing result.
          #
          # If you'd rather have the test runner fail the test in the
          #  absence of either tests or examples, uncommenting either of
          #  the following lines (as appropriate) will enforce that.

          # EXPECT_EXAMPLES: true
          # EXPECT_UNITTESTS: true
```

### Status Badges

You can show Arduino CI status with a badge in your repository `README.md`

```markdown
[![Arduino CI](https://github.com/<OWNER>/<REPOSITORY>/workflows/Arduino%20CI/badge.svg)](https://github.com/marketplace/actions/arduino_ci)
```

> Note that
> * you must replace `<OWNER>` with your GitHub username
> * you must replace `<REPOSITORY>` with the name of the GitHub repository
> * `Arduino%20CI` in the URL must match the `name: Arduino CI` line in the example YAML files above
