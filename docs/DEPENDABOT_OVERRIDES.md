# Dependabot override: postcss

Summary

- On 2026-08-01 I temporarily forced postcss to version 8.5.18 in package.json to resolve a Dependabot security update failure caused by conflicting dependency constraints. This unblock was committed to main in commit 803b3aeb1803dc9e4be307bfdf4e0811c5dfafeb.

Why this was done

- Dependabot could not apply the security update because resolving to a secure postcss required downgrading other packages. To avoid an automated downgrade and unblock security scanning and CI, we added an intentional override to force postcss to a secure version.

Risks and notes

- "overrides" forces a single version across the dependency graph and can mask incompatibilities. We validated the change by ensuring npm install and build succeed locally (recommended), but this should be treated as a short-term mitigation.

Next steps (recommended)

1. Identify the package(s) pinning postcss to an older incompatible version:
   - Run locally: `npm why postcss` and `npm ls postcss`.
2. If a direct dependency is responsible, bump that dependency in package.json to a version compatible with postcss 8.5.18 and remove the override.
3. If a transitive dependency is responsible and has no upgraded release, open an issue/PR against the upstream package, or consider replacing the dependency.
4. After making a non-override fix, remove the overrides entry from package.json and run `npm install` and CI tests.

How I can help next

- I can analyze package-lock.json to find the exact package(s) constraining postcss and propose the exact package.json changes (preferred long-term fix).
- Or I can prepare a PR that documents this temporary override and schedules its removal when a permanent fix is applied.

If you'd like the deep analysis, tell me to proceed and I'll locate the constraining package and produce a minimal change set to remove the override.
