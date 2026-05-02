# Sentinel's Security Journal

## 2025-05-23 - Broken/Incomplete SSRF Protection
**Vulnerability:** The SSRF protection logic was partially implemented but broken, preventing compilation and potentially leaving a false sense of security. It contained redundant and syntactically incorrect checks for IPv6 addresses inside a loop.
**Learning:** Broken security code is worse than no security code because it blocks development while offering no protection. Redundant logic (re-implementing checks that a helper function already does) increases the surface area for bugs.
**Prevention:** Centralize security checks in helper functions (like `is_safe_ip`) and rely on them exclusively. Ensure all security features are fully implemented and tested (including compilation) before merging.

## 2026-03-02 - DNS Rebinding TOCTOU Vulnerability Fix
**Vulnerability:** The SSRF protection mechanism had a Time-of-Check Time-of-Use (TOCTOU) vulnerability. The `is_safe_url` function validated the DNS resolution to ensure the IP was safe, but then used a shared `reqwest::blocking::Client` with the original URL, triggering a second DNS resolution. This allowed a DNS rebinding attack where the attacker's DNS server returns a safe IP during validation and an internal IP during the fetch.
**Learning:** Validating a URL and then fetching it natively without pinning the validated IP is inherently vulnerable to DNS Rebinding.
**Prevention:** Create a new HTTP client pinned specifically to the validated IP using `reqwest::blocking::ClientBuilder::new().resolve(...)`. This ensures the actual request uses the exact IP that was validated, mitigating TOCTOU and SSRF bypasses.

## 2026-03-20 - Arithmetic Safety and DoS Prevention
**Vulnerability:** The interpreter used standard Rust arithmetic operators (+, -, *, /) which panic on division by zero or integer overflow (in debug mode). This could be exploited to cause a Denial of Service (DoS) by crashing the interpreter with malicious scripts.
**Learning:** Interpreters must never trust that arithmetic operations will succeed, especially when dealing with user-provided numbers. Rust's default behavior is to panic in some cases, which is unsuitable for a long-running or multi-tenant interpreter.
**Prevention:** Use checked arithmetic methods (`checked_add`, `checked_sub`, `checked_mul`, `checked_div`) and handle the `None` case by reporting a language-level error instead of allowing the host process to panic.
