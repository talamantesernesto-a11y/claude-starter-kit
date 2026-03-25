# Defense-in-Depth Validation

## Overview

When you fix a bug caused by invalid data, adding validation at one place feels sufficient. But that single check can be bypassed by different code paths.

**Core principle:** Validate at EVERY layer data passes through. Make the bug structurally impossible.

## The Four Layers

### Layer 1: Entry Point Validation
Reject obviously invalid input at API boundary.

### Layer 2: Business Logic Validation
Ensure data makes sense for this operation.

### Layer 3: Environment Guards
Prevent dangerous operations in specific contexts (e.g., refuse git init outside tmpdir in tests).

### Layer 4: Debug Instrumentation
Capture context for forensics (stack traces, state logging).

## Why Multiple Layers

All four layers are necessary. During testing, each layer catches bugs the others miss:
- Different code paths bypass entry validation
- Mocks bypass business logic checks
- Edge cases on different platforms need environment guards
- Debug logging identifies structural misuse

**Don't stop at one validation point.** Add checks at every layer.
