# Minecraft Mod Datapack Template

This repository is a resource-packaging template for distributing a Minecraft
Java datapack with metadata for multiple mod loaders. It contains an example
advancement and loader descriptors; it is not a complete gameplay mod or a
verified compatibility matrix. The original instructions are retained below
for reference, but the source-specific cautions in this section take precedence.

## Repository contents

- `src/main/resources/data/exampledatapack/advancements/root.json` is an example
  advancement; replace the namespace and content with your own datapack.
- `src/main/resources/pack.mcmeta` is a template for datapack metadata.
- `src/main/resources/META-INF/mods.toml` and `neoforge.mods.toml` provide
  low-code Forge/NeoForge descriptors. `fabric.mod.json` and `quilt.mod.json`
  provide Fabric/Quilt descriptors. Their `${...}` values are placeholders.
- `gradle.properties` supplies the example ID, name, version, URLs, license
  metadata and format values. `build.gradle` expands these values into the five
  descriptors, adds generated resources when present, and excludes the
  generated-resource cache from the JAR.
- `gradlew`, `gradlew.bat` and `gradle/wrapper/` provide a Gradle 8.7 wrapper.

## Customize and build

1. Replace the example `mod_*` values and `pack_format*` values in
   `gradle.properties`; check them against the **specific game and loader
   versions** you support. The checked-in properties name Minecraft `1.20.2`
   and NeoForge `20.2.88`, while the datapack format values are `41`, `41` and
   `999`. These values are template settings, not evidence that every version
   in that interval is compatible.
2. Replace `data/exampledatapack/` with your own datapack resources and review
   each loader descriptor. The Fabric descriptor depends on
   `fabric-resource-loader-v0`; the Quilt descriptor accepts
   `quilt_resource_loader` or the named Fabric resource loader. Actual loader
   and API requirements should be verified for your target installation.
3. For the Gradle path, provide a JDK and run `./gradlew build` on Unix-like
   systems or `gradlew.bat build` on Windows. `build.gradle` requests a Java 17
   toolchain, and the wrapper/plugin/dependencies may require network access.
   Build output is normally under `build/libs/`; inspect the resulting archive
   before publishing it. A JAR is a ZIP-format archive, but renaming alone does
   not prove that it is a valid or compatible datapack on a target version.
4. If packaging the resource directory manually instead of using Gradle,
   substitute **all** placeholders in `pack.mcmeta` and the four loader
   descriptors first, and validate the resulting metadata. The unexpanded
   `pack.mcmeta` is not valid JSON. The descriptors reference `pack.png`, but
   this snapshot does not include that file; provide or remove the reference as
   appropriate. Test both archive variants in the intended environments.

The original notes mention that hosting both identical archives may be rejected
as duplicate files; check the current requirements of the hosting service before
publishing. No loader, Minecraft server, Gradle build or published artifact was
tested as part of this README update.

## License and attribution

The repository includes the [CC0 1.0 dedication](LICENSE). The example
`mod_license=All Rights Reserved` in `gradle.properties` is a **template value
for generated mod metadata**, not a replacement for the repository license;
set it deliberately for your own distribution. The historical template link
and contributor guidance are retained in the original text below.

## Historical README (preserved)

The following is the previous README, kept verbatim for continuity. It contains
unverified broad compatibility claims and may not reflect the source details
or cautions above.

~~~~~~text
# Minecraft Mod Datapack Template

This template offers a foundation for creating mod variants of datapacks compatible with major mod loaders including
Forge, NeoForge, Fabric, and Quilt (Fabric API required for Fabric and Quilt). It simplifies the process for developers
to craft datapacks that seamlessly operate as mods in Minecraft.

## Features

- Universal compatibility: Works seamlessly with all Minecraft mod loaders, including Forge, NeoForge, Fabric, and
  Quilt, requiring no specific mod loader.
- Seamless integration with existing datapack structures: Allows for easy integration of additional features into
  existing datapack setups without the need for extensive restructuring.
- **Important note for Fabric and Quilt:** Fabric API is necessary for loading the "mod" as a datapack; without it, the
  mod datapack will not work.

## Prerequisites

- Java Development Kit (JDK) is recommended but not necessary
- Basic knowledge of Minecraft datapack creation and modding

## Usage

1. [Use this template](https://github.com/sa-shiro/Minecraft-Mod-Datapack-Template/generate) to instantly create a new
   GitHub repository based on this template. (optional)
2. Clone or download this or the newly created repository to your local machine.
3. Customize the datapack according to your requirements.
    - To make modifications to the datapack, edit the content of the `src/main/resources` directory.
    - To modify mod/datapack information (such as name, description, etc.), edit the `gradle.properties` file.
4. Build the project:
    - If using Java JDK:
        - Execute the command `gradlew build`.
        - Locate the output JAR file under `build/libs`.
        - Copy and rename the generated JAR to `.zip` for the datapack version.
    - If **NOT** using Java JDK:
        - Ensure to modify the following files: `pack.mcmeta`, `mods.toml`, `neoforge.mods.toml`, `fabric.mod.json`,
          and `quilt.mod.json`, as their information is retrieved using variables from the buildscript and
          the `gradle.properties` file.
        - Compress the contents of the `src/main/resources` folder into a ZIP archive.
        - Rename the compressed ZIP archive to `.jar` for the mod version.
5. Once built, upload both the built JAR file and the renamed ZIP copy to your mod hosting platform.

### Important Note for CurseForge Uploads

When uploading both the mod and datapack variants to CurseForge, ensure that at least one of the files includes an
additional file or modification to prevent rejection due to duplicate files. CurseForge's hashing check will identify
duplicates, resulting in rejection if the hashes match. Adding a dummy file, for instance, is one way to achieve this
differentiation.

## Contributing

Contributions are welcome! If you have suggestions, feature requests, or bug reports, please open an issue or submit
a pull request.

## License

This project is licensed under the [CC0 1.0 Universal (CC0 1.0) Public Domain Dedication](LICENSE).
~~~~~~
