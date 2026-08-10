To disable ESLint during the build process, you have several options:

## Option 1: Environment Variable (Quickest)

Run the build with ESLint disabled:

```bash
# Windows (Command Prompt)
set DISABLE_ESLINT_PLUGIN=true && npm run build

# Windows (PowerShell)
$env:DISABLE_ESLINT_PLUGIN="true"; npm run build

# macOS/Linux
DISABLE_ESLINT_PLUGIN=true npm run build
```

## Option 2: Create `.env` File (Permanent)

Create a `.env` file in your project root and add:

```
DISABLE_ESLINT_PLUGIN=true
```

Then run:
```bash
npm run build
```

## Option 3: Modify `package.json`

Add a new build script that disables ESLint:

```json
{
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "build:no-eslint": "DISABLE_ESLINT_PLUGIN=true react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  }
}
```

Then run:
```bash
npm run build:no-eslint
```

## Option 4: Override Webpack Config (Advanced)

If you're using `react-scripts`, create a `.env` file:

```
ESLINT_NO_DEV_ERRORS=true
DISABLE_ESLINT_PLUGIN=true
```

## Option 5: Ignore ESLint Warnings (Only Warnings)

If you want to keep ESLint but ignore warnings:

```bash
# Set to ignore warnings during build
CI=false npm run build
```

**⚠️ Warning:** While these methods will allow your build to complete, it's generally not recommended to disable ESLint completely as it helps catch potential bugs and maintain code quality. A better approach is to fix the actual ESLint errors or use inline comments to disable specific rules:

```jsx
// eslint-disable-next-line react-hooks/exhaustive-deps
useEffect(() => {
  fetchAdmins();
}, []);
```

Or disable the rule for the entire file:
```jsx
/* eslint-disable react-hooks/exhaustive-deps */
```

**For your specific case**, I recommend either:
1. Fixing the ESLint errors using the `useCallback` solution provided earlier
2. Or using `// eslint-disable-next-line` comments on specific lines if you're sure the code works correctly
