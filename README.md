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

Before running the AGP workflow, configure these in your repository settings:

- **Variable** `AGP_DOCKER_IMAGE` → Internal tag of the AGP Docker image
- **Secret** `AGP_API_TOKEN` → PAT for guide-dev

## Running the Test

1. Configure the required variables and secrets
2. Go to Actions → AGP workflow
3. Click "Run workflow"
4. Verify that AGP creates PRs for all three ecosystems

## Notes

- The workflow runs on `self-hosted` runners
- The `.gitignore` is critical to prevent `dotnet build` artifacts from polluting AGP's PRs
- No `go.sum` is committed - AGP will regenerate it
