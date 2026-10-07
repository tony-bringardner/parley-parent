# parley-parent

The shared Maven parent POM of **Parley**, a family of Java libraries for implementing internet
protocols. Every Parley module inherits from it, so the common settings live in one place:

- Coordinates under `us.bringardner.parley`, and the metadata Maven Central requires: name, URL,
  Apache 2.0 license, developer and SCM (each module's URL and SCM point at its own GitHub repo).
- Java 11 (`maven.compiler.release`), UTF-8, and plugin versions.
- Checks on every build: Maven 3.6.3+, Java 11+, and that each jar module sets `parley.moduleName`
  (written to the jar as `Automatic-Module-Name`).
- A `release` profile with everything a Maven Central release needs: sources and Javadoc jars, GPG
  signatures and the Central Portal publishing plugin.

## Using it

```xml
<parent>
    <groupId>us.bringardner.parley</groupId>
    <artifactId>parley-parent</artifactId>
    <version>1.0.0-SNAPSHOT</version>
</parent>

<artifactId>parley-example</artifactId>
<properties>
    <parley.moduleName>us.bringardner.parley.example</parley.moduleName>
</properties>
```

## Releasing a module to Maven Central

```
mvn -Prelease clean deploy
```

This needs a GPG key (passphrase in `MAVEN_GPG_PASSPHRASE`) and a Central Portal user token in
`~/.m2/settings.xml` under the server id `central`. Uploads wait for you to press Publish on
central.sonatype.com. Release this parent before any module that uses it.

## Modules

parley-core, parley-io, parley-net, parley-files (with parley-files-ftp, -sftp and -jdbc),
parley-ftp, parley-dns, parley-ssh, parley-mail, parley-smtp, parley-imap and parley-pop3.
Their versions are listed together in [parley-bom](https://github.com/tony-bringardner/parley-bom).
