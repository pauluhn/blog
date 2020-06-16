# Why is `/usr/bin/codesign` hanging?

Are your CI builds hanging? 

Do your build logs stop at `/usr/bin/codesign --force --sign <REDACTED> --verbose ~/Library/Developer/Xcode/DerivedData/<REDACTED>/Build/Intermediates.noindex/ArchiveIntermediates/App/InstallationBuildProductsLocation/Applications/App.app/Frameworks/libswift*.dylib`?

Did you try adding fastlane actions like `setup_ci` or `setup_circle_ci`?

Are you using a custom keychain instead of fastlane's `match`?

Did you learn everything there is to know about the `security` command?

Are you using `Apple Distribution`?

...

Welcome to that last corner of the Internet on the last-ish page of Google results!

If you answered `YES` to all/most/any of the above, **The Answer** (at least for my issue) is the automagic of fastlane's `import_certificate`!

```ruby
Fastfile

import_certificate(
  keychain_name: ENV['DEFAULT_KEYCHAIN'],
  keychain_password: ENV['KEYCHAIN_PASSWORD'],
  certificate_path: "*.cer")
  
import_certificate(
  keychain_name: ENV['DEFAULT_KEYCHAIN'],
  keychain_password: ENV['KEYCHAIN_PASSWORD'],
  certificate_path: "*.p12",
  certificate_password: ENV['CERTIFICATE_PASSWORD'])
```

see [fastlane docs](https://docs.fastlane.tools/actions/import_certificate/)
