# Standing agent rules


1. Start from a reproducible baseline. Record the exact source versions and checksums where applicable. Preserve the originals, build and test on separate copies, and prove the workflow with one small change before expanding scope.

2. Define what done means before implementation. Give each change observable acceptance criteria and each milestone a checklist. Advance milestones when their checks pass. Report measured coverage separately from estimates of overall completion.

3. Verify through normal use. Exercise the affected workflow with ordinary user inputs and check the existing behavior it depends on. Record the tested build, environment, setup, actions, and actual results. Identify debugger-assisted checks, fallbacks, exceptions, and anything still untested. For visual changes, use matched before-and-after captures with short captions.

4. Integrate every change through a focused pull request. Branch from current main and use a PR for code, docs, fixes, and rollbacks. Include scope, rationale, acceptance criteria, verification, deployment, and rollback details. Update affected docs in the same PR. Use a merge commit to keep the change independently revertible, and merge through the authorized process once checks pass or the owner accepts a documented exception.

5. Reproduce and verify the release. Build from clean inputs using the documented procedure. Test the packaged candidate from a fresh start, check that required data survives packaging, and verify the installed artifact on the target. Record the deployed version or checksum. If a rollback affects deployment, rebuild, verify, and redeploy the intended version.

6. Decide what ships and what stays local. Publish the source, build recipe, tooling, and instructions needed to reproduce the release. For source-only projects, keep third-party inputs, extracted assets, and generated packages local. Verify the release language and labeling, retain the latest verified preview and original inputs, and clean up superseded test artifacts and sessions.

7. Report progress with evidence. Use the project thread to record what passed, what remains, any limitations, and the relevant PR or commit. Report verified checkpoints at the agreed cadence. Close the project when the published instructions reproduce the release and the final audit is complete.
