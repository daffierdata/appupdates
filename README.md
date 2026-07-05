# App Updates Repository

This repository hosts the update endpoints (`.json` files) and release binaries (`.exe`, `.sig`) for your Tauri applications.

## Releasing an Update for SpecTools

When you are ready to release a new version of SpecTools to your users, follow these steps:

1. **Build the Update**
   In your main `spectools` project directory, bump the version number in `package.json` and `src-tauri/tauri.conf.json`.
   Then, run the build command:
   ```bash
   npm run tauri build
   ```

2. **Retrieve the Built Assets**
   Tauri will generate your new installer and its cryptographic signature in `src-tauri/target/release/bundle/nsis/`.
   - `SpecTools_1.x.x_x64-setup.exe`
   - `SpecTools_1.x.x_x64-setup.exe.sig`

3. **Upload the Installer (.exe) to GitHub**
   - Go to your public GitHub repository (`appupdates`) in the browser.
   - Click "Releases" -> "Draft a new release".
   - Type in the new version number (e.g., `v1.0.1`).
   - Drag and drop the `SpecTools_1.x.x_x64-setup.exe` file you just built into the release box.
   - Click **Publish Release**.
   - Right-click the newly uploaded `.exe` file link on GitHub and click **Copy Link**.

4. **Update the JSON (`spectools.json`)**
   Open the `spectools.json` file in this repository using VSCode.
   - Change `"version"` to match your new version (e.g., `"1.0.1"`).
   - Change `"notes"` to describe the update.
   - Open the `.sig` file generated in Step 2, copy all the text inside, and paste it into the `"signature"` field in the JSON.
   - Paste the `.exe` download link you copied in Step 3 into the `"url"` field.

5. **Push the JSON to GitHub**
   Commit your changes to the JSON file and push them:
   ```bash
   git add spectools.json
   git commit -m "Update SpecTools to v1.0.1"
   git push origin main
   ```

That is it! As soon as you push that JSON file, all of your installed apps will read the new URL and signature, and automatically update!
