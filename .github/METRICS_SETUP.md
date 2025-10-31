# GitHub Metrics Setup Guide

This repository uses [lowlighter/metrics](https://github.com/lowlighter/metrics) to generate a metrics SVG that displays on the profile README.

## Current Status

✅ The workflow runs successfully every 6 hours
⚠️ Some plugins may show errors in logs due to token scope limitations

## Token Configuration

The workflow uses the `METRICS_TOKEN` secret for authentication.

### Required Scopes

For all plugins to work correctly, the token needs the following scopes:

- ✅ **`repo`** (currently configured)
- ⚠️ **`read:user`** (needed for: activity, habits, sponsors plugins)
- ⚠️ **`read:org`** (needed for: activity, habits, sponsors plugins)

### How to Update Token Scopes

If you see errors like "INSUFFICIENT_SCOPES" in the workflow logs:

1. Go to [GitHub Token Settings](https://github.com/settings/tokens)
2. Find and edit the token used for `METRICS_TOKEN`
3. Add the `read:user` and `read:org` scopes
4. Click "Update token"
5. Copy the token (if regenerated)
6. Update the repository secret at: `https://github.com/Lutra-Fs/Lutra-Fs/settings/secrets/actions`

### Alternative: Disable Problematic Plugins

If you don't want to update token scopes, you can disable specific plugins in `.github/workflows/metrics.yml`:

```yaml
plugin_activity: no   # Disable activity plugin
plugin_habits: no     # Disable habits plugin  
plugin_sponsors: no   # Disable sponsors plugin
```

## Troubleshooting

### Common Errors

#### "INSUFFICIENT_SCOPES" Error
**Cause:** Token missing `read:user` or `read:org` scopes  
**Solution:** Update token scopes (see above)

#### "Cannot read properties of undefined" Error
**Cause:** Plugin compatibility issue or missing data  
**Solution:** Disable the affected plugin or update token scopes

#### Workflow Fails to Commit
**Cause:** Missing `contents: write` permission  
**Solution:** Already configured correctly in the workflow

## Workflow Schedule

The metrics are updated automatically:
- **Every 6 hours** (at 00:00, 06:00, 12:00, 18:00 UTC)
- **On every push** to `main` or `master` branch
- **Manually** via workflow_dispatch

## Enabled Plugins

Current configuration includes:

- ✅ Base metrics (header, activity, community, repositories, metadata)
- ✅ Activity plugin (14 days, limit 5)
- ✅ Habits plugin (14 days, with facts)
- ✅ Introduction plugin
- ✅ IsoCalendar plugin (half-year)
- ✅ Languages plugin (most-used languages)
- ✅ Sponsors plugin
- ✅ Stack Overflow plugin (user: 9907854)
- ✅ Stars plugin (limit 4)
- ✅ Topics plugin (starred, limit 15)
- ✅ WakaTime plugin (requires WAKATIME_TOKEN secret)

## Further Reading

- [Metrics Action Documentation](https://github.com/lowlighter/metrics)
- [GitHub Token Scopes](https://docs.github.com/en/apps/oauth-apps/building-oauth-apps/scopes-for-oauth-apps)
