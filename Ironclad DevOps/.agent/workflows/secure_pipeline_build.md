---

#### **Path: `.agent/workflows/`**
**File Name:** `secure_pipeline_build.md`

This workflow enforces the rigid multi-stage structure required by your context.

```markdown
# Workflow: Construct Secure Pipeline

**Trigger:** "New pipeline", "Create release", "Build CICD"

## Step 1: Definition & Governance
1.  **Define Agent Pool:** Hardcode `Agents_on_Windows_VM`.
2.  **Define Variables:** Link the project's Variable Group (No hardcoded secrets!).

## Step 2: Build Stage (The Producer)
* **Checkout:** Self.
* **Compile:** Use local VSBuild/MSBuild.
* **Test:** Unit tests only (Mock external calls).
* **Manifest:** Run "Skill 2" to generate `version.json`.
* **Publish:** `PublishBuildArtifacts@1` to `drop`.

## Step 3: Deployment Strategy (The Consumer)
Create the following stages in order. Use `dependsOn` to enforce sequence.
1.  **Stage: Validate_Artifact** (Check checksums).
2.  **Stage: PreDeploy** (Dry-run, Snapshot Backups).
3.  **Stage: Deploy_Test** (Automated deploy).
4.  **Stage: Deploy_UAT** (Requires `ManualValidation` task).
5.  **Stage: Deploy_Prod** (Requires `ManualValidation` task + Executive Approval).

## Step 4: Final Review Checklist
* [ ] Are external URLs removed?
* [ ] Is `version.json` generated?
* [ ] Is the "Manual Validation" task present for Prod?

## Output
Provide the full YAML file, broken down by templates if the file exceeds 200 lines.