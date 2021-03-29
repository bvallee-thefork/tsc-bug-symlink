# Bug Description

When encountering a symlink directory, and when a `"**/file"` glob is present in the `"include": ["src/**/*"]` config, then files that are not directly imported by other source files are ignored (they are not present in the `tsc --listFiles` output).

# Reproduction steps

With `"include": ["src/**/*]`, `src/symlink/file2.ts` is correctly listed in the output of: `npx tsc -p tsconfig-valid.json --listFiles`

With `"include": ["**/file", "src/**/*]`, `src/symlink/file2.ts` is not listed in the output of: `npx tsc -p tsconfig.json --listFiles`

Note that this seems to happen only because of the symlink, as `src/normal/file2.ts` is correctly present in both outputs.
