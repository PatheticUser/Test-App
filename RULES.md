# Project Rules — AI Coding Agents

**Version:** 1.0  
**Status:** Mandatory  
**Applies To:** Antigravity, Claude Code, and all AI coding agents working on this project.

---

## 1. Purpose and Authority

This document defines mandatory rules for AI coding agents working on the project management application.

The objective is to ensure that all generated code is accurate, secure, maintainable, and consistent with the project's requirements and architecture.

Every agent must follow these rules regardless of its model, tools, capabilities, or operating environment.

### 1.1 Source of Truth

The following documents define the project's requirements and architecture:

1. `Project Requirements Document.md` — product requirements and scope.
2. `architecture.md` — technical architecture and implementation decisions.
3. `Rules.md` — coding, security, and agent behavior requirements.

The actual repository, database schema, migrations, and existing implementation define the current technical state.

When information conflicts:

- Never silently choose one interpretation.
- Identify the conflicting information.
- Follow the most specific applicable requirement when the conflict is minor and unambiguous.
- Ask for clarification when the conflict affects security, architecture, data integrity, or product behavior.
- Do not modify foundational requirements without explicit approval.

The existence of a requirement does not mean that its implementation already exists.

---

## 2. Anti-Hallucination Rules

These rules are mandatory.

### 2.1 Never Invent Facts

Agents must not fabricate:

- Existing files, directories, components, or functions.
- Database tables, columns, relationships, or migrations.
- Environment variables or configuration values.
- API endpoints, request formats, or response structures.
- Supabase features, SDK methods, or MCP tools.
- Package names, package versions, or library capabilities.
- Test results, build results, or deployment status.
- User requirements or previously approved decisions.

If a required fact is unknown, inspect the repository, documentation, or available tools.

If it cannot be verified, explicitly identify it as unknown.

### 2.2 Distinguish Facts From Assumptions

Agents must distinguish between:

- Verified facts.
- Proposed implementation decisions.
- Unverified assumptions.
- Missing information.

Never present an assumption as an established project requirement.

When an assumption is necessary, state it clearly and keep it isolated so it can be changed easily.

### 2.3 Verify APIs Before Using Them

Before using an unfamiliar API, SDK method, framework feature, or MCP tool:

1. Inspect the installed package version.
2. Consult the relevant official documentation or available type definitions.
3. Verify the method signature and expected behavior.
4. Check compatibility with the existing implementation.
5. Implement and test the integration.

Do not invent method names based on naming conventions.

Do not assume that an API exists because a similar API exists in another library or version.

### 2.4 No Fabricated Verification

Agents must never claim that something:

- Works.
- Compiles.
- Passes tests.
- Is secure.
- Is deployed.
- Is synchronized.
- Is fully implemented.

unless the relevant verification was actually performed.

If verification was not possible, state exactly what remains unverified.

---

## 3. Repository Inspection Rules

Before making changes, agents must understand the existing codebase.

### 3.1 Mandatory Inspection

Inspect:

- The project root.
- Package manager and lockfile.
- Existing folder structure.
- Relevant source files.
- Existing components and utilities.
- Database migrations.
- Supabase configuration.
- Environment variable examples.
- Relevant tests.
- Applicable project documentation.

Use the existing implementation as the starting point.

Do not assume the repository is empty or identical to a previous project.

### 3.2 Preserve Existing Work

Agents must not:

- Delete unrelated files.
- Replace entire files when a targeted edit is sufficient.
- Overwrite user changes.
- Reformat unrelated files unnecessarily.
- Reset Git history.
- Discard uncommitted work.
- Remove existing functionality without approval.

Before large changes, inspect the Git diff and current working tree.

If existing changes may belong to the user, preserve them.

### 3.3 No Unnecessary Rewrites

Prefer the smallest complete change that satisfies the requirement.

Do not introduce a new architecture, framework, package, or abstraction when the existing implementation already supports the requirement.

Do not rewrite working functionality simply because a different implementation is preferred.

---

## 4. Requirement and Scope Control

### 4.1 Implement Only What Is Requested

Agents must not silently introduce:

- Additional product features.
- Unrequested UI sections.
- New database tables.
- Alternative authentication methods.
- Additional dependencies.
- New backend services.
- Unrequested integrations.

A technically convenient feature is not automatically an approved feature.

If an improvement is valuable but outside the current scope, propose it separately.

### 4.2 No Fake Implementations

The following are not acceptable as completed functionality:

- Buttons without working actions.
- Forms that do not persist data.
- Mock data presented as production data.
- Hardcoded values presented as database results.
- Placeholder API responses.
- Empty event handlers.
- Simulated authentication.
- Static dashboards presented as live analytics.
- UI-only permission checks.
- Fake real-time synchronization.

A placeholder is acceptable only when explicitly requested or clearly marked as temporary and excluded from completion claims.

### 4.3 No Silent Requirement Changes

Do not change the meaning of an existing requirement to make an implementation easier.

If a requirement is technically infeasible, unsafe, or contradictory, explain the limitation and propose a solution.

---

## 5. Coding Standards

### 5.1 TypeScript

- Use TypeScript throughout the application.
- Avoid `any`.
- Avoid unnecessary type assertions.
- Avoid `@ts-ignore`.
- Avoid non-null assertions when a proper null check is possible.
- Use explicit types for important application boundaries.
- Keep database types synchronized with the actual schema.

Type suppression is permitted only when justified by a verified limitation and documented at the relevant location.

### 5.2 Code Quality

- Use descriptive names.
- Keep functions focused.
- Avoid duplicated business logic.
- Prefer existing shared utilities.
- Handle errors explicitly.
- Validate external input.
- Keep components reasonably small.
- Separate UI logic from data access.
- Avoid unnecessary abstractions.

Do not optimize code based on imagined performance problems.

### 5.3 Dependencies

Before adding a dependency:

1. Verify that the functionality is not already available.
2. Confirm compatibility with the current stack.
3. Check whether the dependency is maintained and appropriate.
4. Explain why the dependency is needed.
5. Use the existing package manager.

Never manually edit the lockfile.

Never install a package with an invented name or version.

---

## 6. Frontend Rules

### 6.1 Design System

All UI must follow the established design system.

Use:

- Tailwind CSS.
- Existing shadcn/ui components.
- Shared design tokens.
- Consistent spacing and typography.
- Existing color variables.
- Reusable application components.

Do not introduce arbitrary colors, spacing systems, or unrelated UI libraries.

### 6.2 No Destructive UI Shortcuts

Never remove functionality to simplify a UI implementation.

Do not hide errors, disable validation, or remove loading states to make an interface appear functional.

Every interactive element must perform its advertised action.

### 6.3 Loading, Empty, and Error States

Every data-driven page must account for:

- Loading.
- Empty results.
- Failed requests.
- Unauthorized access.
- Successful mutations.
- Missing or deleted records.

Do not show an empty state when the actual request failed.

Do not display stale data as current data without an appropriate indication.

### 6.4 Responsive Behavior

All new interfaces must support the project's responsive design requirements.

Do not assume that a desktop layout will automatically work on mobile.

Verify:

- Navigation behavior.
- Overflow.
- Dialog sizing.
- Board scrolling.
- Form usability.
- Touch interactions.

### 6.5 Accessibility

- Use semantic HTML.
- Preserve keyboard navigation.
- Use accessible labels.
- Maintain visible focus indicators.
- Do not rely on color alone.
- Use accessible dialog and dropdown primitives.

Do not replace accessible components with custom implementations without a clear reason.

---

## 7. Supabase and Database Rules

### 7.1 Database Is the Source of Truth

The database is authoritative for persistent application data.

Never use frontend state as a substitute for persisted records.

Do not hardcode workspace IDs, user IDs, project IDs, or task IDs.

Use actual authenticated user and database identifiers.

### 7.2 Schema Verification

Before writing database queries:

- Inspect the actual schema.
- Verify table and column names.
- Verify relationships and foreign keys.
- Verify nullability.
- Verify enum values.
- Verify existing constraints.
- Verify generated TypeScript types.

Do not assume that a table exists because it appears in the PRD or architecture document.

### 7.3 Migrations

Every database schema change must be represented by a version-controlled migration.

Agents must not:

- Modify production schemas directly.
- Create undocumented schema changes.
- Delete tables to resolve migration errors.
- Reset databases without explicit approval.
- Rewrite previously applied migrations without an approved migration strategy.
- Disable constraints to make invalid data insert successfully.

Use additive, backward-compatible migrations where practical.

For destructive changes, document the impact, migration strategy, and recovery plan before proceeding.

### 7.4 Row Level Security

RLS is mandatory for exposed application tables.

Never disable RLS to fix an application error.

Never replace database authorization with frontend-only checks.

Every new table must have appropriate RLS policies before being exposed to application users.

Every new query must be evaluated against the intended user's permissions.

Do not assume that a valid Supabase session automatically grants access to a particular workspace or project.

### 7.5 Supabase Credentials

Never expose:

- Supabase service-role keys.
- Secret API keys.
- Database passwords.
- MCP access tokens.
- Privileged connection strings.

The browser may use the public Supabase key only when the database is protected by appropriate authorization policies.

Never bypass RLS by introducing a privileged client into browser code.

---

## 8. MCP Rules

MCP is a development tool, not an unrestricted database administrator.

### 8.1 Tool Verification

Before calling an MCP tool:

- Verify the tool exists.
- Inspect its actual input schema.
- Confirm the target project and environment.
- Understand whether the operation is read-only or destructive.
- Use only documented arguments.

Never invent MCP tool names, parameters, or capabilities.

Never assume that a successful tool call means the intended database state was achieved.

Verify the resulting state when the operation affects the project.

### 8.2 Database Environment

Agents must distinguish between:

- Local development.
- Remote development.
- Staging.
- Production.

Never assume that the connected Supabase project is the development project.

Verify the target environment before any write operation.

### 8.3 Destructive Operations

The following require explicit approval:

- Dropping tables or columns.
- Resetting databases.
- Deleting production records.
- Disabling RLS.
- Changing production permissions.
- Rotating credentials.
- Running destructive SQL.
- Applying irreversible migrations.

Do not bypass approval by splitting a destructive operation into multiple smaller calls.

Do not perform a destructive operation through another tool merely because the MCP tool requires approval.

### 8.4 MCP Failure Handling

If MCP fails:

- Report the actual error.
- Verify whether the operation partially succeeded.
- Do not claim the operation completed.
- Do not repeatedly retry destructive operations without checking state.
- Do not switch to a privileged workaround without approval.

---

## 9. Security Rules

Security requirements must never be weakened to make development easier.

### 9.1 Authentication

Never:

- Trust a user ID supplied by the browser as proof of identity.
- Trust client-side role values.
- Treat a hidden UI element as authorization.
- Allow unauthorized access because a route is difficult to protect.

Always derive identity from the authenticated session.

### 9.2 Authorization

Every protected operation must verify access to the relevant resource.

For example, task access must account for:

- The authenticated user.
- The task.
- The associated project.
- The workspace.
- The user's membership and permissions.

Do not check workspace membership in one location and assume that all other operations are automatically protected.

### 9.3 Input Validation

Validate data at the appropriate trust boundaries.

Use Zod for frontend form validation and server-side validation where applicable.

Database constraints and RLS must independently enforce data integrity and authorization.

Never trust frontend validation alone.

### 9.4 Error Messages

Do not expose:

- Database credentials.
- Stack traces.
- Internal connection strings.
- Secret environment variables.
- Sensitive database details.

Log useful diagnostic information without exposing sensitive data to users.

---

## 10. Task Management and Real-Time Rules

### 10.1 Task Mutations

Task operations must preserve:

- Task ownership and assignment rules.
- Project membership restrictions.
- Valid task statuses.
- Valid priority values.
- Database constraints.
- Correct task ordering.

Do not update the UI as permanently successful before the mutation is confirmed.

### 10.2 Optimistic Updates

Optimistic updates must:

1. Preserve the previous state.
2. Apply the temporary change.
3. Submit the database mutation.
4. Reconcile with the confirmed result.
5. Roll back on failure.

Never silently discard a failed mutation.

### 10.3 Realtime

Realtime events must be handled safely.

- Scope subscriptions appropriately.
- Clean up subscriptions.
- Avoid duplicate updates.
- Avoid infinite refetch loops.
- Handle reconnection.
- Do not assume events are delivered exactly once.
- Do not assume receiving an event proves that the current user is authorized to access all related data.

RLS must remain authoritative.

---

## 11. Error Handling and Recovery

Agents must not hide failures.

### 11.1 Error Handling

Do not use empty catch blocks.

Do not suppress errors merely to prevent console output.

Do not return fake success responses after a failed operation.

Do not convert authorization failures into empty results without a clear and intentional design decision.

Errors must be handled at the correct layer.

### 11.2 Recovery

If an operation fails:

- Identify the failing layer.
- Inspect the actual error.
- Determine whether the operation partially completed.
- Preserve user data where possible.
- Apply the smallest safe fix.
- Verify the fix.

Do not repeatedly modify unrelated code to eliminate a symptom without understanding its cause.

---

## 12. Testing and Verification

### 12.1 Required Verification

After implementing a feature, perform the relevant checks:

1. TypeScript type checking.
2. Linting.
3. Unit tests.
4. Component tests.
5. Integration tests.
6. Build verification.
7. Manual verification where appropriate.

Run the checks that exist in the repository.

Do not invent commands or claim tests exist without inspecting the project.

### 12.2 Security Testing

For database-related changes, verify:

- Authorized users can perform the intended operation.
- Unauthorized users cannot perform it.
- Users cannot access another workspace's records.
- Users cannot escalate their own permissions.
- Invalid inputs are rejected.
- Privileged credentials are not exposed.

### 12.3 Honest Reporting

Report verification precisely.

Examples:

- "Type checking passed."
- "The build passed."
- "The RLS policy was tested with two user roles."
- "The database migration was created but not applied."
- "The implementation is complete, but browser testing was not performed."

Never claim that the entire application is verified when only one part was tested.

---

## 13. Git and File Safety

Agents must preserve the integrity of the repository.

Never execute the following without explicit approval:

- `git reset --hard`
- `git clean -fd`
- `git checkout -- .`
- `git restore .`
- `git push --force`
- Destructive branch deletion.
- Unreviewed bulk file deletion.

Do not overwrite existing user changes.

Do not commit secrets.

Do not amend or rewrite commits unless requested.

Do not create commits, push branches, or open pull requests unless explicitly authorized.

---

## 14. Autonomous Agent Boundaries

AI coding agents may inspect, plan, implement, and verify tasks within the approved scope.

They must not independently:

- Change the product requirements.
- Replace the selected technology stack.
- Introduce a new backend architecture.
- Remove security controls.
- Modify production infrastructure.
- Delete user data.
- Change authentication behavior.
- Introduce paid services.
- Perform irreversible operations.
- Expand the project into unrelated features.

When a task requires a decision outside the approved scope, stop and request clarification.

Do not interpret a broad instruction such as "finish the project" as permission to make every possible architectural or product decision.

---

## 15. Implementation Workflow

Every substantial task must follow this workflow.

### Step 1 — Understand

- Read the relevant requirements.
- Inspect the existing implementation.
- Identify affected files and systems.
- Identify dependencies and constraints.

### Step 2 — Plan

- Define the intended outcome.
- Identify the smallest complete implementation.
- Identify security implications.
- Identify required database changes.
- Identify required tests.

### Step 3 — Implement

- Make targeted changes.
- Follow the established architecture.
- Reuse existing components.
- Avoid unrelated modifications.
- Preserve existing functionality.

### Step 4 — Verify

- Inspect the final diff.
- Run relevant checks.
- Verify database behavior.
- Verify authorization where applicable.
- Confirm that no unrelated files changed.

### Step 5 — Report

Provide a concise completion report containing:

- What was implemented.
- Important files changed.
- Database changes, if any.
- Tests and checks actually performed.
- Remaining limitations.
- Any unverified behavior.

Do not claim completion when a required step remains unfinished.

---

## 16. Definition of Done

A task is complete only when:

- The requested functionality is implemented.
- The implementation follows the approved architecture.
- No fake functionality remains.
- Existing functionality is preserved.
- Inputs are validated.
- Relevant authorization requirements are enforced.
- Errors are handled appropriately.
- Relevant tests and checks have been performed.
- The final diff contains only intended changes.
- Remaining limitations are explicitly documented.

A feature that only works in a happy-path demonstration is not considered complete.

A feature that bypasses security requirements is not considered complete.

A feature that has not been verified must not be reported as verified.

---

## 17. Mandatory Agent Instruction

Before making any change, read and follow this document.

When requirements, implementation details, or tool capabilities are uncertain, verify them rather than inventing an answer.

When verification is impossible, state the limitation.

When an operation is destructive or outside the approved scope, obtain explicit approval.

When an implementation fails, investigate the actual cause rather than hiding the error or weakening the requirements.

**Correctness, security, data integrity, and honest reporting take priority over speed, convenience, and apparent completion.**
