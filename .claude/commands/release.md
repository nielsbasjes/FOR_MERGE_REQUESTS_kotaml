# Release

Perform a full release of kotaml. The user provides the new version as an argument: `$ARGUMENTS`

If `$ARGUMENTS` is empty, read the current version from `gradle.properties` and ask the user what the new version should be.

## Steps

Execute these steps sequentially. Stop and report if any step fails.

### 1. Update version

Update the `version=` line in `gradle.properties` to the new version.

Search `README.md` for any occurrences of the old version string and replace them with the new version.

### 2. Run publish.sh

```bash
bash publish.sh
```

This builds, signs, publishes artifacts, and uploads the bundle to Sonatype Central.

### 3. Commit

Stage `gradle.properties` and `README.md`, then commit with message:

```
Release v<version>
```

### 4. Create tag

```bash
git tag v<version>
```

### 5. Push

```bash
git push && git push --tags
```

### 6. Create GitHub release

```bash
gh release create v<version> --title "v<version>" --generate-notes
```
