# Angular 21+ UI practices

Apply these defaults to Angular UI code in scope. Follow agreed team standards and established patterns. Confirm a departure before introducing a new pattern; do not refactor unrelated code or change workspace-wide settings just to adopt this guide.

## Scope and readability

- Keep changes cohesive: one purpose per PR. Leave unrelated fixes, features, and refactors out.
- Choose the simplest readable solution that meets the current requirement. Add a service, interface, or helper only when it clarifies a real contract or responsibility or removes meaningful duplication. Avoid speculative reuse.
- Use names that explain intent, including boolean names like `isLoading`, `hasPermission`, and `canEdit`. Avoid unfamiliar abbreviations, deep nesting, and functions that do several unrelated things.

## Angular structure

- Keep templates focused on rendering and user interactions. Move business rules, complex conditions, filtering, sorting, and calculations into TypeScript. Use a pipe for a display transformation where appropriate; avoid calling expensive methods from templates.
- Give each component one UI responsibility. Separate orchestration from presentation when a component becomes hard to follow, and extract child components when they have a clear purpose. Keep data access and reusable rules, mapping, validation, or shared state in focused services or helpers rather than a catch-all service.
- Prefer Angular's built-in tools over custom equivalents: Forms for forms, dependency injection for services, directives for DOM behavior, pipes for display transforms, and router guards for navigation rules.
- Use inputs, outputs, or an explicit service or shared-state contract to communicate. Do not rely on another component's internals. Before importing across libraries, check that the dependency belongs in the architecture and uses an intended public API.

## Reactive data flow

- Use signals for local UI state such as selection, filters, visibility, or loading. Use Observables for asynchronous streams such as HTTP requests. Derive values from their sources rather than manually keeping several copies in sync.
- Keep computed signals simple and their dependencies easy to trace. Put substantial calculations or business rules in a focused helper or service.
- Avoid nested subscriptions. Compose streams with RxJS operators that match the intended behavior: `switchMap` for the latest request, `concatMap` for ordered work, `mergeMap` for independent concurrent work, `forkJoin` for one combined result after all sources complete, and `combineLatest` for combinations that update as sources emit.

## TypeScript contracts

- Type API payloads, form models, configuration, component inputs, and service results. Declare return types for public methods. Prefer inference for clear local types and interfaces, aliases, or simple generics for explicit contracts.
- Use `unknown` and narrow it with checks or type guards when the shape is uncertain. Avoid `any` except as a temporary last resort in migrations or third-party integration. Use assertions only when there is a sound guarantee the compiler cannot infer.
- Keep changed code compatible with strict TypeScript; prefer strict mode for new TypeScript configurations. Use `readonly` for values that should not be reassigned, and constants, unions, or enums for fixed sets. Use optional chaining and nullish coalescing where absence is expected, and remove unused imports and types in the code you touch.
