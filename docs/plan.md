# Project Plan

This file tracks the phased roadmap for kernel-anticheat-lab.

## Phase 0 — Foundations
C/C++ at the systems level, x86-64 basics, Windows user-mode fundamentals (processes, threads, handles, PE format), debugging tools (x64dbg).

## Phase 1 — Lab setup
Windows VM, Visual Studio + WDK install, test-signing enabled, WinDbg kernel debugging configured, "hello world" driver loading and unloading cleanly.

## Phase 2 — Sample game + server
Small authoritative client/server game (fixed tick rate, client-side prediction, interpolation) to act as the protected target.

## Phase 3 — Driver core
Device object, IRP_MJ_CREATE/CLOSE/DEVICE_CONTROL, IOCTL definitions, user-mode service bridging driver and server, Driver Verifier enabled throughout.

## Phase 4 — Process/handle/module monitoring
ObRegisterCallbacks for handle filtering, PsSetCreateProcessNotifyRoutineEx, PsSetLoadImageNotifyRoutine, PsSetCreateThreadNotifyRoutine.

## Phase 5 — Integrity + telemetry
Code-section hashing, self-integrity checks, signed/MAC'd heartbeat telemetry to the server.

## Phase 6 — Server-side detection
Movement/fire-rate validation, aim statistics, anomaly scoring (starting with z-scores).

## Phase 7 — Hardening + write-up
IOCTL input validation, device ACL restricting access to the service, IOCTL fuzzing, threat model and findings write-up.

---

Notes, findings, and deviations from this plan go in dated entries below as the project progresses.
