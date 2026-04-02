# Removing Comments from the Project
 
This guide explains how to remove all comments (`//` and `/* */`) from the JS/JSX source files.
 
---
 
## Option 1: PowerShell (Windows)
 
```powershell
cd finance-dashboard
 
Get-ChildItem -Path src -Recurse -Include *.js,*.jsx | ForEach-Object {
    $content = Get-Content $_.FullName -Raw
    # Remove multi-line comments
    $content = [regex]::Replace($content, '/\*[\s\S]*?\*/', '')
    # Remove single-line comments (preserve URLs like http://)
    $content = [regex]::Replace($content, '(?<!:)//(?!/)[^\n]*', '')
    # Clean up excessive blank lines
    $content = [regex]::Replace($content, '(\r?\n){3,}', "`n`n")
    Set-Content -Path $_.FullName -Value $content -NoNewline
}
```
 
## Option 2: macOS / Linux (Bash)
 
```bash
cd finance-dashboard
 
find src -type f \( -name "*.js" -o -name "*.jsx" \) -exec sed -i '' \
  -e 's|//.*$||g' \
  -e '/\/\*/,/\*\//d' {} +
```
 
## Option 3: Node.js Script
 
Create `remove-comments.mjs` in the project root:
 
```js
import { readdir, readFile, writeFile } from 'fs/promises';
import { join, extname } from 'path';
 
const SRC_DIR = 'src';
const EXTENSIONS = new Set(['.js', '.jsx']);
 
async function getFiles(dir) {
  const entries = await readdir(dir, { withFileTypes: true });
  const files = [];
  for (const entry of entries) {
    const fullPath = join(dir, entry.name);
    if (entry.isDirectory()) files.push(...(await getFiles(fullPath)));
    else if (EXTENSIONS.has(extname(entry.name))) files.push(fullPath);
  }
  return files;
}
 
function removeComments(code) {
  code = code.replace(/\/\*[\s\S]*?\*\//g, '');
  code = code.replace(/(?<!:)\/\/(?!\/)[^\n]*/g, '');
  code = code.replace(/\n{3,}/g, '\n\n');
  return code.trim() + '\n';
}
 
const files = await getFiles(SRC_DIR);
for (const file of files) {
  const content = await readFile(file, 'utf-8');
  await writeFile(file, removeComments(content));
  console.log(`Cleaned: ${file}`);
}
console.log(`\nDone. Processed ${files.length} files.`);
```
 
Run it:
```bash
node remove-comments.mjs
```
 
---
 
## After Removing Comments
 
```bash
# Verify the build still works
npm run build
 
# Test the dev server
npm run dev
```
 
## Files Affected
 
```
src/
├── components/*.jsx
├── context/AppContext.jsx
├── data/transactions.js
├── pages/*.jsx
├── utils/helpers.js
├── App.jsx
└── main.jsx
```
 
> **Note:** `index.css` is excluded — Tailwind directives like `@import` and `@custom-variant` can resemble comments but are functional code.
