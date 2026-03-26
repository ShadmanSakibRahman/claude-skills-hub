---
description: Implement encryption with AES-256, TLS 1.3, key management, envelope encryption, and secure hashing
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert cryptography engineer. Your task is to implement proper encryption for data at rest and in transit, with secure key management practices.

## Steps

1. **Assess encryption requirements**: Identify sensitive data in the application (PII, financial data, health records, credentials) and determine compliance requirements (GDPR, HIPAA, PCI DSS, SOC 2). Map where sensitive data is stored, transmitted, and processed.

2. **Encryption at rest** (database fields, files, backups):
   - Use AES-256-GCM for authenticated encryption (provides confidentiality and integrity)
   - Generate a unique initialization vector (IV/nonce) per encryption operation (12 bytes for GCM)
   - Store ciphertext as: `iv + authTag + encryptedData` (or use a structured format)
   - Node.js: `crypto.createCipheriv('aes-256-gcm', key, iv)`
   - Python: `from cryptography.fernet import Fernet` or `cryptography.hazmat` for AES-GCM
   - Go: `crypto/aes` with `cipher.NewGCM()`
   - Java: `Cipher.getInstance("AES/GCM/NoPadding")`
   - Never use ECB mode; avoid CBC without HMAC (use GCM or CCM instead)

3. **Envelope encryption** (for scalable key management):
   - Generate a Data Encryption Key (DEK) per record or per entity
   - Encrypt the DEK with a Key Encryption Key (KEK) stored in a KMS (AWS KMS, GCP KMS, Azure Key Vault, HashiCorp Vault)
   - Store the encrypted DEK alongside the ciphertext
   - On decryption: call KMS to decrypt the DEK, then use DEK to decrypt data
   - This limits KMS calls and allows key rotation without re-encrypting all data

4. **Key management**:
   - Never hardcode encryption keys in source code
   - Use a dedicated KMS or secrets manager for key storage
   - Implement key rotation policy (90 days) with support for multiple active key versions
   - Tag ciphertexts with key version to support decryption during rotation
   - Separate keys by environment (dev/staging/prod); use different KMS keys
   - Implement key access logging and auditing
   - Define key destruction policy with retention period

5. **Encryption in transit**:
   - Enforce TLS 1.2+ for all external connections
   - Use TLS for internal service-to-service communication (mutual TLS/mTLS for zero-trust)
   - Pin certificates or use private CA for internal services
   - Configure database connections with TLS (`sslmode=verify-full` for PostgreSQL)
   - Enable TLS for Redis, RabbitMQ, and other internal services

6. **Hashing and password storage**:
   - Passwords: Argon2id (memory=64MB, iterations=3, parallelism=4) or bcrypt (cost=12)
   - Integrity verification: SHA-256 or SHA-3 for file checksums and data integrity
   - HMAC: Use HMAC-SHA256 for message authentication and webhook signature verification
   - Never use MD5 or SHA1 for security purposes
   - Use constant-time comparison (`crypto.timingSafeEqual`) to prevent timing attacks

7. **Secure random number generation**:
   - Use cryptographic RNG for all security-sensitive randomness
   - Node.js: `crypto.randomBytes()`, `crypto.randomUUID()`
   - Python: `secrets.token_bytes()`, `secrets.token_hex()`
   - Go: `crypto/rand.Read()`
   - Never use `Math.random()` or `random.random()` for security purposes
   - Generate tokens with at least 128 bits of entropy

8. **Output**: Implement encryption/decryption utility modules, update data access layers to encrypt sensitive fields, configure key management integration, and document the encryption architecture with key rotation procedures.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
