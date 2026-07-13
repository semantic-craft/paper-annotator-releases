# Paper Annotator Releases

Public Sparkle update feed and signed macOS release artifacts for
[Paper Annotator](https://github.com/semantic-craft/paper-annotator).

The app reads this stable feed URL:

`https://raw.githubusercontent.com/semantic-craft/paper-annotator-releases/main/appcast.xml`

## Publish a release

1. On the trusted release Mac, build and notarize the app from the private source
   repository with the feed URL above and its configured `PA_SPARKLE_PUBLIC_KEY`.
2. Put the ZIP and matching Markdown release notes in a staging directory, then
   generate the signed archive entry and signed feed with the Sparkle Keychain key:

   ```sh
   apps/desktop/src-tauri/sparkle-bin/generate_appcast \
     --download-url-prefix https://github.com/semantic-craft/paper-annotator-releases/releases/download/v<version>/ \
     --embed-release-notes \
     <staging-directory>
   ```

   Do not edit the generated appcast afterward; `SURequireSignedFeed` requires
   its trailing signature to match exactly. Never export or upload the private key.
3. Create a published GitHub Release here with tag `v<version>` and upload the
   signed archive. The appcast enclosure URL must point to that immutable asset.
4. Add the new item to `appcast.xml`, commit and push it to `main`. Publish the
   GitHub Release before the appcast entry so users never see a broken download.

Release assets belong in GitHub Releases, not in this Git repository history.
Public Sparkle update feed and release artifacts for Paper Annotator
