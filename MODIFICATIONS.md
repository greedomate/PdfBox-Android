# PdfBox-Android Fork Modifications

This is a fork of TomRoush's PdfBox-Android with modifications to replace the deprecated JCenter repository dependency.

## Original Repository
- **Source**: https://github.com/TomRoush/PdfBox-Android
- **License**: Apache License 2.0
- **Original Author**: TomRoush

## Fork Repository  
- **Fork**: https://github.com/greedomate/PdfBox-Android
- **License**: Apache License 2.0 (maintained)
- **Fork Author**: greedomate

## Modifications Made

### 1. JP2ForAndroid Integration Fix (Phase 1)
**Problem**: Original project used `com.gemalto.jp2:jp2-android:1.0.3` from JCenter, which shut down in May 2021. The JitPack build of JP2ForAndroid was failing due to Bintray shutdown and signing configuration issues.

**Solution**: 
- Forked JP2ForAndroid repository (https://github.com/greedomate/JP2ForAndroid)
- Fixed JP2ForAndroid JitPack build issues:
  - Removed signing configuration from testapp/build.gradle
  - Commented out problematic testapp from settings.gradle 
  - Fixed build structure for JitPack compatibility
- Updated PdfBox-Android dependency from JCenter to JitPack: `com.github.greedomate:JP2ForAndroid:1.0.3`
- Added proper BSD-2-Clause attribution for JP2ForAndroid

**Files Changed**:
- `sample/build.gradle` - Updated dependency from JCenter to JitPack
- `NOTICE.txt` - Added JP2ForAndroid license attribution
- Repository: Forked JP2ForAndroid at https://github.com/greedomate/JP2ForAndroid

### 2. JitPack Repository Configuration (Phase 2)
**Problem**: PdfBox-Android wasn't configured to work with modern dependency resolution and JitPack.

**Solution**:
- Added JitPack repository support to enable fetching forked dependencies
- Removed deprecated `jcenter()` dependencies completely
- Updated README.md to reference JitPack instead of JCenter

**Files Changed**:
- Root `build.gradle` - Removed jcenter() references
- `README.md` - Updated JP2ForAndroid integration instructions

### 3. Gradle Repository Configuration Migration (Phase 3)
**Problem**: JitPack builds were failing due to repository configuration conflicts between `dependencyResolutionManagement` and project-level repositories.

**Solution**:
- Migrated from project-level repositories to centralized `dependencyResolutionManagement` in `settings.gradle`
- Used `RepositoriesMode.FAIL_ON_PROJECT_REPOS` to ensure consistent dependency resolution
- Created `jitpack.yml` for Java version specification to prevent JDK compatibility issues

**Files Changed**:
- `settings.gradle` - Added dependencyResolutionManagement with centralized repositories
- `build.gradle` - Removed duplicate repository definitions from allprojects block
- `jitpack.yml` - Added Java 11 configuration for JitPack compatibility

### 4. Apache 2.0 License Compliance Documentation
**Problem**: Forking Apache 2.0 licensed project requires proper documentation of modifications.

**Solution**:
- Added comprehensive fork notice documentation
- Created detailed modification history
- Maintained original Apache license attribution
- Documented all technical changes and solutions

**Files Changed**:
- `NOTICE.txt` - Added fork notice and modification list
- `README.md` - Added fork attribution and modification links
- `MODIFICATIONS.md` - Created detailed documentation (this file)

### 5. Final Dependency Reference Cleanup (Phase 4.1)
**Problem**: JitPack build failing due to remaining old dependency references in library module and documentation.

**Solution**:
- Updated library/build.gradle compileOnly dependency from JCenter to JitPack
- Fixed README.md JP2Android integration instructions 
- Ensured all dependency references point to forked JP2ForAndroid version
- Added proper repository configuration examples in documentation

**Files Changed**:
- `library/build.gradle` - Updated compileOnly dependency from `com.gemalto.jp2:jp2-android:1.0.3` to `com.github.greedomate:JP2ForAndroid:c1bc02214b`
- `README.md` - Updated JP2Android integration section with JitPack repository configuration

### 6. JitPack Dependency Commit Hash Resolution (Phase 4.2)
**Problem**: JitPack build failing because version tag `1.0.3` was not working, needed to use specific commit hash.

**Solution**:
- Identified that JP2ForAndroid fork works with commit hash `c1bc02214b` instead of version tag `1.0.3`
- Updated all dependency references to use working commit hash for JitPack compatibility
- Ensured both library module and sample module use consistent commit hash reference

**Files Changed**:
- `library/build.gradle` - Updated compileOnly dependency to use commit hash `c1bc02214b`
- `sample/build.gradle` - Updated implementation dependency to use commit hash `c1bc02214b` 
- `README.md` - Updated integration instructions to show correct commit hash
- `NOTICE.txt` - Documented commit hash resolution in modification list

### 3. Legal Compliance
- Maintained Apache 2.0 license compliance
- Added proper BSD-2-Clause attribution for JP2ForAndroid dependency
- Documented all modifications per Apache license requirements

## Technical Benefits
- ✅ JPX image support restored (was broken due to JCenter shutdown)
- ✅ JitPack compatibility for easier dependency management
- ✅ Modern Gradle dependency resolution
- ✅ Legal compliance maintained

## Usage
This fork can be used as a drop-in replacement for the original PdfBox-Android:

```gradle
dependencies {
    implementation 'com.github.greedomate:PdfBox-Android:commit-hash'
}
```

Repository configuration:
```gradle
repositories {
    mavenCentral()
    google()
    maven { url 'https://jitpack.io' }
}
```

## License
This fork maintains the original Apache License 2.0. All modifications are documented above as required by the Apache license terms.
