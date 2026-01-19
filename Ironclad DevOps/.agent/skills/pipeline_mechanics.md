---

#### **Path: `.agent/skills/`**
**File Name:** `pipeline_mechanics.md`

This file provides the technical implementation details for the "Offline" and "Validation" requirements.

```markdown
# Agent Skills: Pipeline Mechanics & Offline Ops

## Skill 1: Air-Gapped Tool Resolution
**Trigger:** "Install package", "Run tests", "Build solution"
**Capability:**
Translate standard online commands into offline equivalents using local paths.
* **NuGet:** Replace `NuGetCommand@2` (restore) with `vstsFeed` (local) or explicit path `-Source C:\LocalNugetCache`.
* **npm:** Replace `npm install` with `npm ci --offline` pointing to a committed `node_modules` cache or local registry.
* **Test Runner:** Use `VSTest@2` pointed specifically at `test.dll` files in the build output, strictly excluding network-dependent integration tests.

## Skill 2: Artifact Integrity & Manifest Generation
**Trigger:** "Create manifest", "Verify checksum", "Audit trail"
**Capability:**
Generate and verify cryptographic proof of artifacts using PowerShell.
* **Generation Logic (Build Phase):**
  ```powershell
  $manifest = @{
      BuildId = $(Build.BuildId)
      GitHash = $(Build.SourceVersion)
      Timestamp = (Get-Date).ToString("u")
      Artifacts = Get-ChildItem -Recurse | Get-FileHash -Algorithm SHA256
  }
  $manifest | ConvertTo-Json | Out-File "version.json"