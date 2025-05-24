# maven-slf4j-main-starter [![ci](https://github.com/daggerok/maven-slf4j-main-starter-java-21/actions/workflows/ci.yml/badge.svg)](https://github.com/daggerok/maven-slf4j-main-starter-java-21/actions/workflows/ci.yml)
Maven application project starter using maven wrapper, slf4j, assertj and java 21 (tested on Zulu and GraalVM)

## Getting Started

Create a new project

```bash
npx --yes degit daggerok/maven-slf4j-main-starter-java-21 my-app && cd $_
```

## Setup Development Environment

Install Java 21

```bash
brew reinstall zulu@21 # graalvm@21

declare -f use # output:
function use() {
	function usage() {
		echo "Usage:\n\tuse jdk 1.8\nor:\n\tuse graalvm 21"
		return
	}
	if [[ $# -eq 0 ]] ; then
		usage
		return -1
	fi
	if [[ $# -eq 2 ]] ; then
		USE_WHAT=${1:-jdk}
		if [[ "jdk" != "$USE_WHAT" && "graalvm" != "$USE_WHAT" ]] ; then
			usage
			return -2
		fi
		export JAVA_VERSION=${2:-21}
	else
		export JAVA_VERSION=${1:-21}
	fi
	if [[ "graalvm" == "$USE_WHAT" ]] ; then
		export JAVA_HOME=/Library/Java/JavaVirtualMachines/graalvm-$JAVA_VERSION.jdk/Contents/Home
	else
		export JAVA_HOME=$(/usr/libexec/java_home -v $JAVA_VERSION)
	fi
	export PATH=$JAVA_HOME/bin:$PATH
	return 0
}
```

## Test Build Run

```bash
use zulu 21 ; java -version
./mvnw clean ; ./mvnw ; java -jar target/*.jar
```
