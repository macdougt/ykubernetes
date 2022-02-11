[Helm charts](https://helm.sh/docs/topics/charts/)

A chart is a packaging format

Format:

Charts are created as files laid out in a particular directory tree. They can be packaged into versioned archives to be deployed.

Chart Strcuture
---------------

Sample:

```
wordpress/
  Chart.yaml          # A YAML file containing information about the chart
  LICENSE             # OPTIONAL: A plain text file containing the license for the chart
  README.md           # OPTIONAL: A human-readable README file
  values.yaml         # The default configuration values for this chart
  values.schema.json  # OPTIONAL: A JSON Schema for imposing a structure on the values.yaml file
  charts/             # A directory containing any charts upon which this chart depends.
  crds/               # Custom Resource Definitions
  templates/          # A directory of templates that, when combined with values,
                      # will generate valid Kubernetes manifest files.
  templates/NOTES.txt # OPTIONAL: A plain text file containing short usage notes
```
[Chart file fields](https://helm.sh/docs/topics/charts/#the-chartyaml-file) with sample for postgres:

```yaml
apiVersion: The chart API version (required)
name: The name of the chart (required)
version: A SemVer 2 version (required)
kubeVersion: A SemVer range of compatible Kubernetes versions (optional)
description: A single-sentence description of this project (optional)
type: The type of the chart (optional)
keywords:
  - A list of keywords about this project (optional)
home: The URL of this projects home page (optional)
sources:
  - A list of URLs to source code for this project (optional)
dependencies: # A list of the chart requirements (optional)
  - name: The name of the chart (nginx)
    version: The version of the chart ("1.2.3")
    repository: (optional) The repository URL ("https://example.com/charts") or alias ("@repo-name")
    condition: (optional) A yaml path that resolves to a boolean, used for enabling/disabling charts (e.g. subchart1.enabled )
    tags: # (optional)
      - Tags can be used to group charts for enabling/disabling together
    import-values: # (optional)
      - ImportValues holds the mapping of source values to parent key to be imported. Each item can be a string or pair of child/parent sublist items.
    alias: (optional) Alias to be used for the chart. Useful when you have to add the same chart multiple times
maintainers: # (optional)
  - name: The maintainers name (required for each maintainer)
    email: The maintainers email (optional for each maintainer)
    url: A URL for the maintainer (optional for each maintainer)
icon: A URL to an SVG or PNG image to be used as an icon (optional).
appVersion: The version of the app that this contains (optional). Needn't be SemVer. Quotes recommended.
deprecated: Whether this chart is deprecated (optional, boolean)
annotations:
  example: A list of annotations keyed by name (optional).
```

Here is a sample for [postgres](https://github.com/helm/charts/blob/master/stable/postgresql/Chart.yaml):

```yaml
apiVersion: v1
name: postgresql
version: 8.6.4
appVersion: 11.7.0
# The postgresql chart is deprecated and no longer maintained. For details deprecation, see the PROCESSES.md file.
deprecated: true
description: DEPRECATED Chart for PostgreSQL, an object-relational database management system (ORDBMS) with an emphasis on extensibility and on standards-compliance.
keywords:
  - postgresql
  - postgres
  - database
  - sql
  - replication
  - cluster
home: https://www.postgresql.org/
icon: https://bitnami.com/assets/stacks/postgresql/img/postgresql-stack-110x117.png
sources:
  - https://github.com/bitnami/bitnami-docker-postgresql
maintainers: []
engine: gotpl
```

## [Templates and values](https://helm.sh/docs/topics/charts/#templates-and-values)

All template files are stored in a chart's templates/ folder. When Helm renders the charts, it will pass every file in that directory through the template engine.

Values for the templates are supplied two ways:

Chart developers may supply a file called values.yaml inside of a chart. This file can contain default values.
Chart users may supply a YAML file that contains values. This can be provided on the command line with helm install.
When a user supplies custom values, these values will override the values in the chart's values.yaml file.

[Template files](https://helm.sh/docs/topics/charts/#template-files)

 - Follows [golang templates style](https://golang.org/pkg/text/template/)

