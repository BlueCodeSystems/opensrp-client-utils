# opensrp-client-utils

Shared utilities, form contracts, and UI configuration helpers that back OpenSRP Android form workflows and other reusable components.

## Project Status
- Toolchain: Gradle 8.7 · Android Gradle Plugin 8.6.0 · Java (JDK 17) · Kotlin not required (Java-only module)
- Modules: `opensrp-utils` (library), `app` (sample/demo shell)
- Continuous integration: Travis CI configuration present (`.travis.yml`); verify against your current CI pipeline
- Current branch: `master`; latest tag: `v0.0.7`

## Features
- Contracts that define how client forms are stored, served, and rendered (`ClientFormContract`)
- Exhaustive JSON form constants used across OpenSRP-native form rendering (`JsonFormConstants`)
- A configurable `Form` domain model for branding, navigation, and button behaviors in wizard-style flows

## Requirements
- JDK: 17 (Temurin/OpenJDK recommended)
- Gradle: Wrapper pinned to 8.7 (run via `./gradlew`)
- Android Gradle Plugin: 8.6.0
- Kotlin: Not required (Java sources only)
- Android SDK: `compileSdk` / `targetSdk` 35, `minSdk` 28, Build Tools 35.0.0
- Android Studio: Giraffe or newer recommended for AGP 8.6

## Install
Add the dependency from Maven Central (replace `<version>` with the latest release version).

<details>
<summary>Groovy DSL</summary>

```groovy
repositories {
  mavenCentral()
}

dependencies {
  implementation 'io.github.bluecodesystems:opensrp-client-utils:<version>' // see Releases for versions
}
```

</details>

<details>
<summary>Kotlin DSL</summary>

```kotlin
repositories {
  mavenCentral()
}

dependencies {
  implementation("io.github.bluecodesystems:opensrp-client-utils:<version>") // see Releases for versions
}
```

</details>

> If you consume this repository as a multi-module project, you can instead depend on `project(":opensrp-utils")`.

## Initialize
No global initialization hook is required. Add the dependency and exercise the APIs directly in your feature modules.

## Usage examples
Configure a form shell for a native JSON workflow:

```java
import org.smartregister.client.utils.domain.Form;

Form registration = new Form();
registration.setName("household_registration");
registration.setWizard(true);
registration.setNextLabel("Next");
registration.setPreviousLabel("Back");
registration.setGreyOutSaveWhenFormInvalid(true);
```

Build JSON field definitions with shared constants:

```java
import org.json.JSONObject;
import org.smartregister.client.utils.constants.JsonFormConstants;

JSONObject householdName = new JSONObject()
    .put(JsonFormConstants.KEY, "household_name")
    .put(JsonFormConstants.TYPE, JsonFormConstants.EDIT_TEXT)
    .put(JsonFormConstants.HINT, "Household name");
```

Implement a lightweight DAO for client forms:

```java
import java.util.ArrayList;
import java.util.List;
import org.smartregister.client.utils.contract.ClientFormContract;

public class InMemoryClientFormDao implements ClientFormContract.Dao {
  private final List<ClientFormContract.Model> cache = new ArrayList<>();

  @Override
  public void addOrUpdate(ClientFormContract.Model clientForm) {
    cache.removeIf(existing -> existing.getId() == clientForm.getId());
    cache.add(clientForm);
  }

  @Override
  public ClientFormContract.Model getActiveClientFormByIdentifier(String identifier) {
    return cache.stream()
        .filter(ClientFormContract.Model::isActive)
        .filter(model -> identifier.equals(model.getIdentifier()))
        .findFirst()
        .orElse(null);
  }

  // Implement other contract methods to persist forms to disk, SQLCipher, etc.
}
```

## Sample app
The `app/` module acts as a minimal harness. To install it on a connected device or emulator:

```bash
./gradlew :app:installDebug
```

You can also open the project in Android Studio and use the standard run configurations targeting the `app` module.

## Build & test
- Assemble all variants: `./gradlew clean assemble`
- Run unit tests (includes the library placeholder test suite): `./gradlew test`
- Generate Jacoco coverage for the library: `./gradlew :opensrp-utils:jacocoTestReport`

## Releases
Binary releases and changelogs are published under [GitHub Releases](https://github.com/BlueCodeSystems/opensrp-client-utils/releases). Check the latest tag before updating `<version>` in your build.

## Contributing
Issues and pull requests are welcome. Please:
- Use JDK 17, Gradle 8.7, and AGP 8.6.0 when building locally
- Run `./gradlew clean assemble test` before submitting a PR
- Follow existing code style and package structure for contracts and constants

If you add significant features or fixes, update this README with new guidance.

## License
Apache License 2.0 — see [LICENSE](LICENSE) for the full terms.
