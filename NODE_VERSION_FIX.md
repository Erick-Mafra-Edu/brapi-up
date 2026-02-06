# Node.js Version Compatibility Fix

## Problem
The application was experiencing a build failure with the error:
```
Error [ERR_PACKAGE_PATH_NOT_EXPORTED]: Package subpath './lib/parser' is not defined by "exports"
```

This occurred when building with Node.js v24.13.0 because Next.js 10.0.6 and its bundled dependencies (particularly postcss-scss) are incompatible with Node.js v24's stricter module resolution requirements.

## Solution
The project has been configured to use Node.js 16.x, which is fully compatible with Next.js 10.0.6 and all project dependencies.

### Changes Made
1. **Created `.nvmrc`** - Specifies Node.js 16 for local development
2. **Updated `vercel.json`** - Added `nodeVersion: "16.x"` for Vercel deployments
3. **Updated `package.json`** - Added `engines` field to document Node.js version requirements

### For Local Development
If using nvm (Node Version Manager):
```bash
nvm use
```

Or manually install Node.js 16:
```bash
nvm install 16
nvm use 16
```

### For CI/CD and Deployment
- Vercel will automatically use Node.js 16.x based on `vercel.json` configuration
- Other platforms should respect the `engines` field in `package.json`
- If needed, explicitly set Node.js 16.x in your CI/CD configuration

### Verification
Build should now succeed without the ERR_PACKAGE_PATH_NOT_EXPORTED error:
```bash
yarn build
```

## Future Considerations
To use newer Node.js versions, consider upgrading:
- Next.js from 10.0.6 to latest version (13.x or 14.x)
- All dependencies to their latest compatible versions
- This would be a larger migration but would enable use of Node.js 18+ or 20+
