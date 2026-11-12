# expo-doctor + devEngines.packageManager repro

A blank app from `create-expo-app --template blank`. The only change is a `devEngines.packageManager` entry pointing to pnpm in `package.json`, plus `expo-doctor` as a dev dependency.

```bash
pnpm install
pnpm expo-doctor
```

Three checks fail because expo-doctor runs `npm explain <pkg> --json`, and npm refuses to run with `EBADDEVENGINES` when `devEngines.packageManager` isn't npm:

```
Error: Failed to find dependency tree for react-native-vector-icons: npm explain react-native-vector-icons --json exited with non-zero code: 1
```

Remove the `devEngines` block and all 20 checks pass.
