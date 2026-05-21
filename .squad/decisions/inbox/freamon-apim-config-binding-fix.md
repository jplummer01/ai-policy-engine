# 2026-05-21 — APIM ResourceId env binding convention

**Owner:** Freamon  
**Status:** proposed  
**Requested by:** Zack Way

## Context

`ApimManagementOptions` binds from the `Apim` configuration section, so the API expects the APIM resource ID at config key `Apim:ResourceId`. The Container App Terraform wiring used `APIM_RESOURCE_ID`, which ASP.NET Core does not translate into a nested config key.

## Decision

Use the standard ASP.NET Core environment-variable convention for nested keys: `Apim__ResourceId` (double underscore). Keep the C# options binding unchanged and make Terraform emit the conventional key.

## Why

- Matches the default `EnvironmentVariablesConfigurationProvider` behavior.
- Keeps the application code strict and idiomatic instead of adding one-off alias handling.
- Prevents silent runtime misbinding when infrastructure sets nested config values.

## Impact

Future Terraform and deployment wiring for APIM management should use `Apim__ResourceId` whenever populating `Apim:ResourceId`.
