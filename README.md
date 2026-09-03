# AGP NuGet Fixture

Test fixture for **GUIDE-3514** - validating .NET SDK support in the AGP Docker image.

## Purpose

This repository contains three projects with deliberately **outdated and vulnerable dependencies** to test AGP's ability to generate upgrade PRs across different ecosystems:

- **nuget-app/** - .NET project with a vulnerable NuGet package
- **go-app/** - Go module with a vulnerable dependency
- **python-app/** - Python project with a vulnerable package

## ⚠️ Important Note

**All dependencies are pinned to vulnerable versions ON PURPOSE.** This is a test fixture, not production code.

## Required Configuration

Before running the AGP workflow, configure this in your repository settings:

- **Variable** `AGP_API_URL` → Sonatype Guide environment URL (ej: `https://api.guide-dev.sonatype.dev`)

Note: This workflow uses GitHub OIDC authentication (`id-token: write`), so no `AGP_API_TOKEN` secret is needed.

## Running the Test

1. Configure the `AGP_API_URL` variable
2. Ensure the AGP Docker image with .NET SDK is loaded on the self-hosted runner
3. Go to Actions → "Sonatype Guide - Agent P" workflow
4. Click "Run workflow"
5. Verify that AGP creates PRs for all three ecosystems

## Notes

- The workflow runs on `self-hosted` runners
- The `.gitignore` is critical to prevent `dotnet build` artifacts from polluting AGP's PRs
- No `go.sum` is committed - AGP will regenerate it
