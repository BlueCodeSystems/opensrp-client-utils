# opensrp-client-utils

Utilities and contracts shared across OpenSRP Android projects: contracts, helpers, constants, and general-purpose utilities.

## Installation

Gradle (example coordinates if published for your org):

```
repositories {
  mavenCentral()
  mavenLocal()
}

dependencies {
  implementation 'io.github.bluecodesystems:opensrp-client-utils:<version>'
}
```

Or include as a module dependency:

```
dependencies {
  implementation project(':opensrp-utils')
}
```

## Build

- Prerequisites: Java 11+ and Android SDK; the Gradle wrapper is included.
- Build library AAR: `./gradlew :opensrp-utils:assembleRelease`
- Run sample app: `./gradlew :app:installDebug`
- Publish to local Maven: `./gradlew :opensrp-utils:publishToMavenLocal`

## Contributing

- Keep changes scoped and follow existing style.
- Avoid committing build outputs (`build/`, `.gradle/`).
