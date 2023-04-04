# kogito-demo-quickstart

This project uses Quarkus, the Supersonic Subatomic Java Framework.

If you want to learn more about Quarkus, please visit its website: https://quarkus.io/.

## Business point of view

This is an HR app. It features:

- HR task list
- Vacancy registry
- Resume registry
- Hiring history

In the app we have several processes:

- Submit a vacancy
- Submit a resume
- Vacancy - resume matching and interview planning
- Interview and hiring decision
- Candidate notification

## Architecture

- Kogito app
- Data index
- Job service
- Mongodb as store
- Kafka as event bus
- Task list
- Console
- UI for registries based on graphql
- Mail or sms client (sw + Camel?)

No auth and no keycloack on purpose.

## Init project

```shell
quarkus create app ru.sbertech.bpm.examples:kogito-demo-quickstart:1.0 \
  --extension='kogito, quarkus-resteasy-reactive, quarkus-resteasy-reactive-jackson' \
  --no-code

# be careful with reactive - not all extensions still support reactive, you may face conflict with ordinary resteasy
```

Add additional dependencies, see <https://docs.jboss.org/kogito/release/latest/html_single/#ref-kogito-add-ons_kogito-creating-running>. List of current extensions and addons:

```shell
quarkus extension add \
kogito-addons-quarkus-persistence-mongodb \
kogito-addons-quarkus-messaging \
quarkus-smallrye-reactive-messaging-kafka \
kogito-addons-quarkus-events-decisions \d
kogito-addons-quarkus-events-process \
kogito-addons-quarkus-jobs-management \
kogito-addons-quarkus-monitoring-prometheus \
kogito-addons-quarkus-process-management \
kogito-addons-quarkus-process-svg \
kogito-addons-quarkus-task-management
# quarkus-dashbuilder
```

## Running the application in dev mode

You can run your application in dev mode that enables live coding using:

```shell
./mvnw compile quarkus:dev
```

> **_NOTE:_**  Quarkus now ships with a Dev UI, which is available in dev mode only at http://localhost:8080/q/dev/.

## Packaging and running the application

The application can be packaged using:
```shell script
./mvnw package
```
It produces the `quarkus-run.jar` file in the `target/quarkus-app/` directory.
Be aware that it’s not an _über-jar_ as the dependencies are copied into the `target/quarkus-app/lib/` directory.

The application is now runnable using `java -jar target/quarkus-app/quarkus-run.jar`.

If you want to build an _über-jar_, execute the following command:
```shell script
./mvnw package -Dquarkus.package.type=uber-jar
```

The application, packaged as an _über-jar_, is now runnable using `java -jar target/*-runner.jar`.

## Creating a native executable

You can create a native executable using: 
```shell script
./mvnw package -Pnative
```

Or, if you don't have GraalVM installed, you can run the native executable build in a container using: 
```shell script
./mvnw package -Pnative -Dquarkus.native.container-build=true
```

You can then execute your native executable with: `./target/kogito-demo-quickstart-1.0-runner`

If you want to learn more about building native executables, please consult https://quarkus.io/guides/maven-tooling.

## Related Guides

- Kogito ([guide](https://quarkus.io/guides/kogito)): Add business automation capabilities - processes and rules with Kogito (a toolkit that originates from projects Drools and jBPM)
