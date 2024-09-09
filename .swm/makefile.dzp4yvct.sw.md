---
title: Makefile
---
# Intro

This document explains how to use the <SwmPath>[Makefile](Makefile)</SwmPath> in the root directory of the project. It will cover each target and its purpose in the build process.

<SwmSnippet path="/Makefile" line="1">

---

# Default Target

The default target is <SwmToken path="Makefile" pos="1:4:4" line-data=".PHONY: all">`all`</SwmToken>, which depends on the <SwmToken path="Makefile" pos="2:3:3" line-data="all: develop">`develop`</SwmToken> target. This ensures that running <SwmToken path="Makefile" pos="30:2:2" line-data="	@make devenv-sync">`make`</SwmToken> without arguments will execute the <SwmToken path="Makefile" pos="2:3:3" line-data="all: develop">`develop`</SwmToken> target.

```
.PHONY: all
all: develop
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="4">

---

# Variables

Several variables are defined for convenience: <SwmToken path="Makefile" pos="4:0:0" line-data="PIP := python -m pip --disable-pip-version-check">`PIP`</SwmToken> for pip commands, <SwmToken path="Makefile" pos="5:0:0" line-data="WEBPACK := yarn build-acceptance">`WEBPACK`</SwmToken> for webpack commands, and <SwmToken path="Makefile" pos="6:0:0" line-data="POSTGRES_CONTAINER := sentry_postgres">`POSTGRES_CONTAINER`</SwmToken> for the PostgreSQL container name.

```
PIP := python -m pip --disable-pip-version-check
WEBPACK := yarn build-acceptance
POSTGRES_CONTAINER := sentry_postgres
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="8">

---

# Freeze Requirements

The <SwmToken path="Makefile" pos="8:0:2" line-data="freeze-requirements:">`freeze-requirements`</SwmToken> target runs a Python script to freeze the current Python package requirements.

```
freeze-requirements:
	@python3 -S -m tools.freeze_requirements
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="11">

---

# Bootstrap

The <SwmToken path="Makefile" pos="11:0:0" line-data="bootstrap:">`bootstrap`</SwmToken> target provides instructions for setting up a new development environment. It suggests running <SwmToken path="Makefile" pos="13:15:17" line-data="	@echo &quot;you probably want to run devenv sync to bring the&quot;">`devenv sync`</SwmToken> to update the environment.

```
bootstrap:
	@echo "devenv bootstrap is typically run on new machines."
	@echo "you probably want to run devenv sync to bring the"
	@echo "sentry dev environment up to date!"
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="16">

---

# Scripted Targets

Several targets (<SwmToken path="Makefile" pos="16:0:4" line-data="build-platform-assets \">`build-platform-assets`</SwmToken>, <SwmToken path="Makefile" pos="17:0:0" line-data="clean \">`clean`</SwmToken>, <SwmToken path="Makefile" pos="18:0:2" line-data="init-config \">`init-config`</SwmToken>, etc.) are defined to run specific scripts using a common script runner <SwmPath>[scripts/do.sh](scripts/do.sh)</SwmPath>.

```
build-platform-assets \
clean \
init-config \
run-dependent-services \
drop-db \
create-db \
apply-migrations \
reset-db \
node-version-check :
	@./scripts/do.sh $@
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="27">

---

# Development Targets

The <SwmToken path="Makefile" pos="27:0:0" line-data="develop \">`develop`</SwmToken>, <SwmToken path="Makefile" pos="28:0:4" line-data="install-js-dev \">`install-js-dev`</SwmToken>, and <SwmToken path="Makefile" pos="29:0:4" line-data="install-py-dev :">`install-py-dev`</SwmToken> targets all depend on the <SwmToken path="Makefile" pos="30:4:6" line-data="	@make devenv-sync">`devenv-sync`</SwmToken> target, ensuring the development environment is synchronized.

```
develop \
install-js-dev \
install-py-dev :
	@make devenv-sync
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="34">

---

# Devenv Sync

The <SwmToken path="Makefile" pos="34:4:6" line-data=".PHONY: devenv-sync">`devenv-sync`</SwmToken> target runs the <SwmToken path="Makefile" pos="36:1:3" line-data="	devenv sync">`devenv sync`</SwmToken> command to synchronize the development environment.

```
.PHONY: devenv-sync
devenv-sync:
	devenv sync
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="38">

---

# Build JS PO

The <SwmToken path="Makefile" pos="38:0:4" line-data="build-js-po: node-version-check">`build-js-po`</SwmToken> target ensures the correct Node.js version is used, creates a build directory, clears the Babel cache, and runs the webpack build with translation extraction.

```
build-js-po: node-version-check
	mkdir -p build
	rm -rf node_modules/.cache/babel-loader
	SENTRY_EXTRACT_TRANSLATIONS=1 $(WEBPACK)
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="43">

---

# Build Spectacular Docs

The <SwmToken path="Makefile" pos="43:0:4" line-data="build-spectacular-docs:">`build-spectacular-docs`</SwmToken> target generates the <SwmToken path="Makefile" pos="44:13:13" line-data="	@echo &quot;--&gt; Building drf-spectacular openapi spec (combines with deprecated docs)&quot;">`openapi`</SwmToken> specification using <SwmToken path="Makefile" pos="44:9:11" line-data="	@echo &quot;--&gt; Building drf-spectacular openapi spec (combines with deprecated docs)&quot;">`drf-spectacular`</SwmToken> and validates it.

```
build-spectacular-docs:
	@echo "--> Building drf-spectacular openapi spec (combines with deprecated docs)"
	@OPENAPIGENERATE=1 sentry django spectacular --file tests/apidocs/openapi-spectacular.json --format openapi-json --validate --fail-on-warn
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="47">

---

# Build Deprecated Docs

The <SwmToken path="Makefile" pos="47:0:4" line-data="build-deprecated-docs:">`build-deprecated-docs`</SwmToken> target builds the deprecated <SwmToken path="Makefile" pos="48:11:11" line-data="	@echo &quot;--&gt; Building deprecated openapi spec from json files&quot;">`openapi`</SwmToken> specification from JSON files using a Yarn script.

```
build-deprecated-docs:
	@echo "--> Building deprecated openapi spec from json files"
	yarn build-deprecated-docs
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="51">

---

# Build API Docs

The <SwmToken path="Makefile" pos="51:0:4" line-data="build-api-docs: build-deprecated-docs build-spectacular-docs">`build-api-docs`</SwmToken> target combines the deprecated and spectacular docs, then dereferences the JSON schema for ease of use.

```
build-api-docs: build-deprecated-docs build-spectacular-docs
	@echo "--> Dereference the json schema for ease of use"
	yarn deref-api-docs
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="55">

---

# Watch API Docs

The <SwmToken path="Makefile" pos="55:0:4" line-data="watch-api-docs:">`watch-api-docs`</SwmToken> target installs dependencies and starts a TypeScript watch process for the API docs.

```
watch-api-docs:
	@cd api-docs/ && yarn install
	@cd api-docs/ && ts-node ./watch.ts
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="59">

---

# Diff API Docs

The <SwmToken path="Makefile" pos="59:0:4" line-data="diff-api-docs:">`diff-api-docs`</SwmToken> target compares local API docs against a reference schema using a Yarn script.

```
diff-api-docs:
	@echo "--> diffing local api docs against sentry-api-schema/openapi-derefed.json"
	yarn diff-docs
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="63">

---

# Build Locale

The <SwmToken path="Makefile" pos="63:0:0" line-data="build: locale">`build`</SwmToken> target depends on the <SwmToken path="Makefile" pos="63:3:3" line-data="build: locale">`locale`</SwmToken> target, which is not defined in the provided snippet.

```
build: locale
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="65">

---

# Merge Locale Catalogs

The <SwmToken path="Makefile" pos="65:0:4" line-data="merge-locale-catalogs: build-js-po">`merge-locale-catalogs`</SwmToken> target builds JS PO files, installs Babel, and merges translation catalogs.

```
merge-locale-catalogs: build-js-po
	$(PIP) install Babel
	cd src/sentry && sentry django makemessages -i static -l en
	./bin/merge-catalogs en
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="70">

---

# Compile Locale

The <SwmToken path="Makefile" pos="70:0:2" line-data="compile-locale:">`compile-locale`</SwmToken> target installs Babel, finds good translation catalogs, and compiles messages.

```
compile-locale:
	$(PIP) install Babel
	./bin/find-good-catalogs src/sentry/locale/catalogs.json
	cd src/sentry && sentry django compilemessages
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="75">

---

# Install Transifex

The <SwmToken path="Makefile" pos="75:0:2" line-data="install-transifex:">`install-transifex`</SwmToken> target installs the Transifex client using pip.

```
install-transifex:
	$(PIP) install transifex-client
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="78">

---

# Push Transifex

The <SwmToken path="Makefile" pos="78:0:2" line-data="push-transifex: merge-locale-catalogs install-transifex">`push-transifex`</SwmToken> target merges locale catalogs and pushes new strings to Transifex.

```
push-transifex: merge-locale-catalogs install-transifex
	tx push -s
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="81">

---

# Pull Transifex

The <SwmToken path="Makefile" pos="81:0:2" line-data="pull-transifex: install-transifex">`pull-transifex`</SwmToken> target pulls new translations from Transifex.

```
pull-transifex: install-transifex
	tx pull -a
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="84">

---

# Update Transifex

The <SwmToken path="Makefile" pos="85:0:2" line-data="update-transifex: push-transifex">`update-transifex`</SwmToken> target pushes new strings to Transifex.

```
# Update transifex with new strings that need to be translated
update-transifex: push-transifex

```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="87">

---

# Update Local Locales

The <SwmToken path="Makefile" pos="88:0:4" line-data="update-local-locales: pull-transifex compile-locale">`update-local-locales`</SwmToken> target pulls new translations from Transifex and compiles them.

```
# Pulls new translations from transifex and compiles for usage
update-local-locales: pull-transifex compile-locale
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="90">

---

# Build Chartcuterie Config

The <SwmToken path="Makefile" pos="90:0:4" line-data="build-chartcuterie-config:">`build-chartcuterie-config`</SwmToken> target builds the Chartcuterie configuration module using a Yarn script.

```
build-chartcuterie-config:
	@echo "--> Building chartcuterie config module"
	yarn build-chartcuterie-config
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="94">

---

# Run Acceptance Tests

The <SwmToken path="Makefile" pos="94:0:2" line-data="run-acceptance:">`run-acceptance`</SwmToken> target runs acceptance tests using pytest and generates coverage and report files.

```
run-acceptance:
	@echo "--> Running acceptance tests"
	python3 -b -m pytest tests/acceptance --cov . --cov-report="xml:.artifacts/acceptance.coverage.xml" --json-report --json-report-file=".artifacts/pytest.acceptance.json" --json-report-omit=log --junit-xml=".artifacts/acceptance.junit.xml" -o junit_suite_name=acceptance
	@echo ""
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="99">

---

# Test CLI

The <SwmToken path="Makefile" pos="99:0:2" line-data="test-cli: create-db">`test-cli`</SwmToken> target creates a test configuration, runs various Sentry CLI commands, and cleans up the test directory.

```
test-cli: create-db
	@echo "--> Testing CLI"
	rm -rf test_cli
	mkdir test_cli
	cd test_cli && sentry init test_conf
	cd test_cli && sentry --config=test_conf help
	cd test_cli && sentry --config=test_conf upgrade --traceback --noinput
	cd test_cli && sentry --config=test_conf export
	rm -r test_cli
	@echo ""
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="110">

---

# Test JS Build

The <SwmToken path="Makefile" pos="110:0:4" line-data="test-js-build: node-version-check">`test-js-build`</SwmToken> target checks the Node.js version, runs a TypeScript type check, and builds static assets.

```
test-js-build: node-version-check
	@echo "--> Running type check"
	@yarn run tsc -p config/tsconfig.build.json
	@echo "--> Building static assets"
	@NODE_ENV=production yarn webpack-profile > .artifacts/webpack-stats.json

```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="116">

---

# Test JS

The <SwmToken path="Makefile" pos="116:0:2" line-data="test-js: node-version-check">`test-js`</SwmToken> target runs <SwmToken path="Makefile" pos="117:9:9" line-data="	@echo &quot;--&gt; Running JavaScript tests&quot;">`JavaScript`</SwmToken> tests using a Yarn script.

```
test-js: node-version-check
	@echo "--> Running JavaScript tests"
	@yarn run test
	@echo ""
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="121">

---

# Test JS CI

The <SwmToken path="Makefile" pos="121:0:4" line-data="test-js-ci: node-version-check">`test-js-ci`</SwmToken> target runs CI-specific <SwmToken path="Makefile" pos="122:11:11" line-data="	@echo &quot;--&gt; Running CI JavaScript tests&quot;">`JavaScript`</SwmToken> tests using a Yarn script.

```
test-js-ci: node-version-check
	@echo "--> Running CI JavaScript tests"
	@yarn run test-ci
	@echo ""
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="133">

---

# Test Python CI

The <SwmToken path="Makefile" pos="133:0:4" line-data="test-python-ci:">`test-python-ci`</SwmToken> target runs CI-specific Python tests using pytest and generates coverage and report files.

```
test-python-ci:
	@echo "--> Running CI Python tests"
	python3 -b -m pytest \
		tests \
		--ignore tests/acceptance \
		--ignore tests/apidocs \
		--ignore tests/js \
		--ignore tests/tools \
		--cov . $(COV_ARGS) \
		--json-report \
		--json-report-file=".artifacts/pytest.json" \
		--json-report-omit=log \
		--junit-xml=.artifacts/pytest.junit.xml \
		-o junit_suite_name=pytest
```

---

</SwmSnippet>

<SwmSnippet path="/Makefile" line="154">

---

# Test Monolith <SwmToken path="Makefile" pos="154:4:4" line-data="test-monolith-dbs:">`dbs`</SwmToken>

The <SwmToken path="Makefile" pos="154:0:4" line-data="test-monolith-dbs:">`test-monolith-dbs`</SwmToken> target runs CI-specific Python tests with monolith databases enabled.

```
test-monolith-dbs:
	@echo "--> Running CI Python tests (SENTRY_USE_MONOLITH_DBS=1)"
	SENTRY_LEGACY_TEST_SUITE=1 \
	SENTRY_USE_MONOLITH_DBS=1 \
	python3 -b -m pytest \
	  tests/sentry/backup/test_exhaustive.py \
	  tests/sentry/backup/test_exports.py \
	  tests/sentry/backup/test_imports.py \
	  tests/sentry/backup/test_releases.py \
	  tests/sentry/runner/commands/test_backup.py \
	  --cov . \
	  --cov-report="xml:.artifacts/python.monolith-dbs.coverage.xml" \
	  --json-report \
	  --json-report-file=".artifacts/pytest.monolith-dbs.json" \
	  --json-report-omit=log \
	  --junit-xml=.artifacts/monolith-dbs.junit.xml \
	  -o junit_suite_name=monolith-dbs \
	;
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="general-build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
