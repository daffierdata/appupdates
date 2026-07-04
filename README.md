# App Updates Repository

This repository hosts the update endpoints (`.json` files) and release binaries (`.msi`, `.sig`) for your Tauri applications.

## Releasing an Update for SpecTools

When you are ready to release a new version of SpecTools to your users, follow these steps:

1. **Build the Update**
   In your main `spectools` project directory, bump the version number in `package.json` and `src-tauri/tauri.conf.json`.
   Then, run the build command:
   ```bash
   npm run tauri build
   ```

2. **Retrieve the Built Assets**
   Tauri will generate your new installer and its cryptographic signature in `src-tauri/target/release/bundle/msi/`.
   - `SpecTools_1.x.x_x64_en-US.msi`
   - `SpecTools_1.x.x_x64_en-US.msi.sig`

3. **Update the JSON**
   Open the `spectools.json` file in this repository.
   - Change `"version"` to match your new version (e.g., `"1.0.1"`).
   - Change `"notes"` to describe the update.
   - Open the `.sig` file generated in Step 2 with a text editor, copy its contents, and paste it into the `"signature"` field in the JSON.
   - Update the `"url"` field to point to the new `.msi` file you will upload.

4. **Push to GitHub**
   Commit your changes and push them to this repository:
   ```bash
   git add .
   git commit -m "Update SpecTools to v1.0.1"
   git push origin main
   ```

5. **Upload the Installer (.msi)**
   Go to your GitHub repository in the browser. Go to "Releases" -> "Draft a new release".
   Upload the `SpecTools_1.x.x_x64_en-US.msi` file to the release and publish it!

Your users' apps will immediately see the new `spectools.json` file and prompt them to download the new `.msi`!
