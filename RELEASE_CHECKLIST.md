# Release checklist

## Package

- [x] Marketplace manifest created
- [x] Plugin manifest created
- [x] `prd-workflow-router` included
- [x] Shared `PRD_WORKFLOW_CHECKLIST.md` template included
- [x] Shared `PRD_DECISIONS.md` template included
- [x] `foundation-build-risk-review` included with references
- [x] `define-problem-statement` included with references
- [x] `define-hypothesis` included with references
- [x] `show-me-the-prd` included with all references
- [x] `utility-pm-critic` and `pm-critic` agent included with references
- [x] `deliver-edge-cases` included with references
- [x] `deliver-acceptance-criteria` included with references
- [x] `measure-instrumentation-spec` included with references
- [x] `goaljaby` included with all references
- [x] Shared questioning policy included

## Public-safety review

- [x] Personal home and absolute OpenClaw paths removed
- [x] Internal actor names and representative-only wording removed
- [x] Unbundled marketing, QA, legal, and company workflow dependencies removed
- [x] Secret-pattern scan completed
- [x] External-send and private-data approval gates retained
- [x] Original MIT copyright notice retained
- [x] Apache-2.0 license, attribution, and modification notices retained

## Validation

- [x] Plugin validator passed
- [x] Internal and public router validators passed after state-file update
- [x] All ten skill validators passed for version 0.3.0
- [x] Marketplace JSON parsed successfully
- [x] Version 0.3.0 local marketplace add and plugin install smoke test passed
- [x] Test-only local registration removed after verification

## Publish gate

- [x] Confirm GitHub owner and repository name
- [x] Confirm public visibility for direct-link installation
- [x] Replace the README installation placeholder with the final repository path
- [x] Show the final publish scope and receive explicit text approval
- [x] Create the GitHub repository and push `main`
- [x] Test installation from the GitHub marketplace source
- [x] Keep the repository out of external plugin directories and curated listings
