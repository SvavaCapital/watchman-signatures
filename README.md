# Watchman Signatures

This repository contains signatures that are utilised by the [Slack Watchman tool](https://github.com/SvavaCapital/slack-watchman)

The signatures are stored under /signature folder as .yaml file. 

## Example Signature File

password_detection.yaml

---
filename: password_detection.yaml
signatures:

  - name: Password Detection
    status: enabled
    author: Vikas Rawat
    date: "2024-07-19"
    description: Detects potentially exposed passwords in plaintext based on complexity requirements
    severity: "80"
    notes:
    references:
    watchman_apps:
      slack_std:
        category: pii
        scope:
          - messages
        file_types:
        search_strings:
          - password
      slack_eg:
        scope:
          - messages
          - drafts
        file_types:
        locations:
          - public
          - private
          - connect
        search_strings:
          - password
    test_cases:
      match_cases:
        - "P@ssw0rd"
        - "Secure123"
      fail_cases:
        - "password"
        - "12345678"
    patterns:
      - '\n?(?=.*[A-Z])(?=.*\d)[A-Za-z\d]{8,}\n?'% 
