name: Bug Report 2
description: Report a bug in Optimus
labels: kind/bug
body:
  - type: textarea
    id: warning
    attributes:
      label: ⚠️Warning⚠️
      description: Please report [Security Vulnerability Here](https://github.com/optimisticjc/jubilant-journey/security/policy)
  - type: textarea
    id: description
    validations:
      required: true
    attributes:
      label: Describe the bug
      description: >-
        Describe the issue you are experiencing here to communicate to the
        maintainers. Tell us what you were trying to do and what happened.

        Provide a clear and concise description of what the problem is.
  - type: textarea
    id: expected_behavior
    attributes:
      label: Expected behavior
      description: >-
        Describe the expected behavior clearly and concisely.
  - type: textarea
    id: actual_behavior
    attributes:
      label: Actual behavior
      description: >-
        Describe the actual behavior clearly and concisely.
  - type: textarea
    id: how_to_reproduce
    attributes:
      label: How to Reproduce?
      description: >-
        Link to a small reproducer (preferably a Maven project if the issue is not Gradle-specific) or attach an archive containing the reproducer to the issue.
      placeholder: |
        Reproducer:

        Steps to reproduce the behavior:
        1. 
        2. 
        3.
  - type: markdown
    id: environment
    attributes:
      value: |
        ## Environment
  - type: input
    id: uname
    attributes:
      label: Output of `uname -a` or `ver`
  - type: input
    id: java_version
    attributes:
      label:  Output of `java -version`
  - type: input
    id: graalvm_version
    attributes:
      label:  GraalVM version (if different from Java)
  - type: input
    id: Optimus_version
    attributes:
      label:  Optimus version or git rev
  - type: input
    id: build_tool
    attributes:
      label:  Build tool (ie. output of `mvnw --version` or `gradlew --version`)
  - type: textarea
    id: additional_info
    attributes:
      label: Additional information
      description: >
        If you have any additional information for us, use the field below.
        Please note, you can attach screenshots or screen recordings here, by
        dragging and dropping files in the field below.
