# Deployment Fixes

## Issues Fixed

### 1. GitHub Metrics Workflow Failures

The GitHub metrics workflow was consistently failing due to two main issues:

#### **GitHub Projects (classic) API Deprecation**
- **Problem**: The achievements plugin was trying to access GitHub's deprecated Projects (classic) API
- **Error**: `Projects (classic) is being deprecated in favor of the new Projects experience`
- **Solution**: Disabled the achievements plugin by setting `plugin_achievements: no`
- **Reference**: [GitHub Blog - Sunset Notice for Projects Classic](https://github.blog/changelog/2024-05-23-sunset-notice-projects-classic/)

#### **Lines Plugin Configuration Issue**
- **Problem**: The lines plugin was trying to read properties from undefined objects
- **Error**: `Cannot read properties of undefined (reading 'includes')`
- **Solution**: Added explicit sections configuration with `plugin_lines_sections: base`

### 2. Environment Configuration Simplification

- **Change**: Removed unnecessary environment wrapper configuration
- **Benefit**: Simplified token access and reduced potential configuration conflicts

## Files Modified

- `.github/workflows/metrics.yml` - Updated GitHub metrics workflow configuration

## Testing

Once these changes are merged to the main branch, the metrics workflow should run successfully:

1. The workflow runs automatically every hour
2. It also runs on pushes to the main/master branch
3. It can be manually triggered via workflow_dispatch

## Monitoring

After deployment:
- Check the GitHub Actions tab for successful workflow runs
- Verify the metrics SVG file is being updated properly
- Monitor for any new error messages in the workflow logs