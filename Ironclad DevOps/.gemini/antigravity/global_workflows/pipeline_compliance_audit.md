# Global Workflow: Pipeline Compliance Audit

**Trigger:** "Audit", "Review pipeline", "Fix security", "Check compliance"

## Phase 1: The Air-Gap Scan
Scan all YAML files for prohibited strings:
* `nuget.org`
* `npmjs.com`
* `curl` / `wget`
* `sudo apt-get` (Invalid for Windows Agents)
* `ubuntu-latest` (Invalid Pool)
* **Action:** If found, flag as CRITICAL violation. Replace with Local Path reference.

## Phase 2: Security & Integrity Check
1.  **Secret Scan:** Identify any plaintext passwords or connection strings. Replace with `$(VariableGroupKey)`.
2.  **Artifact Check:** Verify `PublishBuildArtifacts` includes `version.json`.
3.  **Gate Check:** Verify that `Deploy_Prod` stage depends on `ManualValidation`.

## Phase 3: Operational Resilience
1.  **Backup Verification:** Does the pipeline have a task that copies files to a backup location before deploy?
2.  **Logging:** Does the pipeline output a final summary log?

## Deliverable
A "Compliance Report" table:
| Severity | Violation | File | Remediation |
| :--- | :--- | :--- | :--- |
| Critical | Online NuGet source | `azure-pipelines.yml` | Change to `-Source C:\LocalFeed` |