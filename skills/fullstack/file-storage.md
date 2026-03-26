---
description: Set up file storage with S3/R2/MinIO including upload API, presigned URLs, CDN, and image transformation
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in cloud file storage and media management for web applications. When asked to set up file storage, follow these steps:

**Step 1: Choose the Storage Provider**
- **AWS S3**: Industry standard, broadest ecosystem, pay-per-use pricing.
- **Cloudflare R2**: S3-compatible, zero egress fees, excellent for high-bandwidth use cases.
- **MinIO**: Self-hosted S3-compatible, ideal for development and on-premise deployments.
- **Supabase Storage**: Built on S3, integrated with Supabase projects.
- Install the appropriate SDK: `@aws-sdk/client-s3`, `@aws-sdk/s3-request-presigner`.
- Configure environment variables: bucket name, region, access key, secret key, endpoint URL.

**Step 2: Create the Storage Client**
- Create a reusable storage service module (e.g., `lib/storage.ts`).
- Initialize the S3 client with credentials from environment variables.
- For R2/MinIO: set the custom endpoint URL in the client config.
- Create helper functions: `uploadFile`, `deleteFile`, `getSignedUrl`, `listFiles`.
- Handle errors gracefully with proper error types and messages.

**Step 3: Build the Upload API**
- Create an API endpoint for file uploads (e.g., `POST /api/upload`).
- Support two upload methods:
  - **Direct upload**: Receive the file on the server, then forward to S3 (simpler, size-limited).
  - **Presigned URL**: Generate a presigned PUT URL, client uploads directly to S3 (scalable, no server load).
- For presigned URLs: set expiration (5-15 minutes), restrict content type, set max file size.
- Return the file URL, key, and metadata after successful upload.

**Step 4: File Type Validation and Security**
- Validate file types on both client and server (never trust client-side validation alone).
- Create an allowlist of accepted MIME types (e.g., image/jpeg, image/png, application/pdf).
- Check file signatures (magic bytes) to prevent MIME type spoofing.
- Set maximum file size limits per file type (e.g., 5MB for images, 50MB for documents).
- Sanitize filenames: remove special characters, add unique prefixes (UUID or timestamp).
- Scan for malware if handling user uploads in sensitive environments.

**Step 5: CDN Integration**
- Set up a CDN (CloudFront, Cloudflare, or Vercel Edge) in front of the storage bucket.
- Configure the CDN to cache files with appropriate TTL (e.g., 1 year for immutable assets).
- Set proper Cache-Control headers on uploaded files.
- Use a custom domain for the CDN (e.g., `cdn.example.com` or `assets.example.com`).
- Configure CORS on the bucket to allow uploads from the application domain.

**Step 6: Image Transformation**
- Set up on-the-fly image transformation using Cloudflare Images, imgproxy, or Sharp.
- Support common transforms: resize, crop, format conversion (WebP/AVIF), quality adjustment.
- Implement URL-based transforms (e.g., `/images/w_400,h_300,q_80/image.jpg`).
- Generate responsive image srcsets for different screen sizes.
- Cache transformed images to avoid re-processing on every request.

**Step 7: Storage Lifecycle and Management**
- Configure bucket lifecycle rules: transition to cheaper storage tiers after 30 days, delete temporary files after 24 hours.
- Implement soft delete: mark files as deleted in the database, purge from storage after a grace period.
- Track storage usage per user for quota enforcement.
- Create an admin interface or API for browsing and managing stored files.
- Set up backup replication to another region or bucket for critical files.
- Document the storage architecture and URL patterns for the team.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
