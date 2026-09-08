# Dependency admission policy

Third-party dependency versions age for **14 days** before normal admission into an EffortlessMetrics dependency graph.

The cooldown is an admission control, not a substitute for vulnerability scanning, provenance checks, lockfiles, or review.

## Required controls

1. **14-day version cooldown.** Automated version updates must not admit a version published less than 14 days ago. Apply the rule to every supported ecosystem and to direct and transitive resolution where the package manager can enforce it.
2. **Committed lockfile.** Repositories with a resolved dependency graph commit the ecosystem lockfile. Library lockfiles govern the repository's own CI/test graph; published dependency constraints remain independently correct for downstream consumers.
3. **Frozen CI and release resolution.** Ordinary CI and release jobs consume the committed lockfile without implicitly updating it (`cargo <command> --locked`, `npm ci`, pnpm/Bun/uv frozen or locked equivalents, and analogous modes).
4. **Security updates remain immediate.** A known security remediation may bypass the 14-day window. The exception must be bounded to the required package/version and visible in the change or policy record; do not create permanent package-wide exemptions merely to admit one fix.
5. **Keep independent security signals.** Continue vulnerability, malicious-package, license/policy, provenance, and dependency-review checks. Age reduces early-adopter exposure; it does not prove a package safe.
6. **Constrain install-time execution.** Disable or allowlist dependency lifecycle/build-time execution where the ecosystem supports doing so without breaking the build.
7. **Fail closed on policy capability.** A configured control that the active package-manager version does not understand is a policy failure. CI should verify the effective toolchain supports the controls it claims to enforce.

## Update automation

For Dependabot version updates, every `updates` entry should include:

```yaml
cooldown:
  default-days: 14
```

Dependabot security updates bypass this cooldown by design.

For Renovate, use `minimumReleaseAge: "14 days"` and keep release timestamps required. Where Renovate regenerates a lockfile, also enforce the age rule in the package manager when it has a resolver-native control so a newly selected transitive dependency cannot bypass the updater-side gate.

## Rust / Cargo

Until Cargo 1.100 is naturally within the repository toolchain policy, enforce the 14-day boundary in dependency-update automation and keep `Cargo.lock` plus `--locked` CI/release resolution. **Do not raise MSRV merely to acquire Cargo-native minimum-publish-age support.**

When Cargo 1.100 is within policy, add resolver-native minimum publish age as a second boundary rather than replacing the updater cooldown.

## Exceptions

An exception is appropriate when delaying adoption creates more risk than early adoption, most commonly a verified security fix or a required compatibility fix blocking supported tooling. Keep it narrow and record:

- package and exact version;
- reason for early admission;
- evidence supporting the exception; and
- whether any temporary policy relaxation must be removed afterward.

The default remains 14 days.
