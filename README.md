# JVM OpenFaaS Afterburn

[OpenFaas](https://www.openfaas.com/) JVM template supporting [afterburn](https://github.com/openfaas-incubator/of-watchdog#2-afterburn-implemented) with the new watchdog implementation. This is an answer to the cold start problem when using the serverless architecture.

## Build and Deploy to OpenFaaS

* Deploy [OpenFaaS](https://github.com/openfaas/faas#get-started-with-openfaas)

* Install [OpenFaaS CLI](https://github.com/openfaas/faas-cli#get-started-install-the-cli)

* Get the template and create the function and run the sample

```
faas-cli template pull https://github.com/amirkarimi/openfaas-jvm-afterburn-template
faas-cli new --lang jvm-afterburn jvm_burner

faas-cli build -f jvm_burner.yml
faas-cli deploy -f jvm_burner.yml
echo test | faas-cli invoke jvm_burner
```

## Update the function

You just need to generate a JAR file using your favorate langauge and tools, rename the JAR file to `app.jar` and copy to the `function` folder.

* [Scala Sample](https://github.com/amirkarimi/openfaas-scala-afterburn)
* [Java Sample](https://github.com/openfaas/java-afterburn)

## Run watchdog locally

This is useful for testing/debugging purposes.

* Build the new version of watchdog supporting Afterburn. Navigate to another dir.

```
git clone git@github.com:openfaas-incubator/of-watchdog.git \
cd of-watchdog \
./build.sh
```

* Copy `of-watchdog` to a where the main JAR file exists

* Run watchdog:

```
mode=afterburn fprocess="java -jar app.jar" ./of-watchdog
```

* Send the requests to `localhost:8081`
