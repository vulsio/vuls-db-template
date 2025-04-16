# vuls-db-template

This is a template repository for regularly creating your own `vuls.db` using GitHub Actions.

## Usage

By selecting the `db-add` target in `db-build` of the `GNUMakefile`, you can create a `vuls.db` for yourself and upload it to `ghcr.io/<repository owner>/<repository name>`.

For example, if you want to add `mitre-v5` data, change it as follows:

```diff
:100644 100644 5eb2622 0000000 M	GNUMakefile

diff --git a/GNUMakefile b/GNUMakefile
index 5eb2622..6f1e8f1 100644
--- a/GNUMakefile
+++ b/GNUMakefile
@@ -9,6 +9,7 @@ db-build:
 	$(MAKE) -f ${MAKEFILE} db-add REPO=vuls-data-extracted-alma-errata BRANCH=${BRANCH} DBTYPE=${DBTYPE} DBPATH=${DBPATH}
 	$(MAKE) -f ${MAKEFILE} db-add REPO=vuls-data-extracted-redhat-vex-rhel BRANCH=${BRANCH} DBTYPE=${DBTYPE} DBPATH=${DBPATH}
 	$(MAKE) -f ${MAKEFILE} db-add REPO=vuls-data-extracted-rocky-errata BRANCH=${BRANCH} DBTYPE=${DBTYPE} DBPATH=${DBPATH}
+	$(MAKE) -f ${MAKEFILE} db-add REPO=vuls-data-extracted-mitre-v5 BRANCH=${BRANCH} DBTYPE=${DBTYPE} DBPATH=${DBPATH}
 
 .PHONY: db-add
 db-add: 
```

You can find out what data sources are currently available:
```console
$ gh api --paginate /orgs/vulsio/packages/container/vuls-data-db/versions --jq '.[] | select(.metadata.container.tags[] | startswith("vuls-data-extracted-")) | .metadata.container.tags[]'
vuls-data-extracted-redhat-vex-rhel
vuls-data-extracted-redhat-csaf-rhel
vuls-data-extracted-redhat-ovalv2
vuls-data-extracted-redhat-vex
vuls-data-extracted-redhat-csaf
vuls-data-extracted-redhat-ovalv1
vuls-data-extracted-redhat-ovalv2-rhel
vuls-data-extracted-nvd-api-cve
vuls-data-extracted-mitre-v5
vuls-data-extracted-epss
vuls-data-extracted-arch
vuls-data-extracted-amazon
vuls-data-extracted-alma-osv
vuls-data-extracted-alma-errata
vuls-data-extracted-oracle
vuls-data-extracted-alpine-secdb
vuls-data-extracted-alpine-osv
vuls-data-extracted-freebsd
vuls-data-extracted-kev
vuls-data-extracted-rocky-errata
```

Or you can refer to this list.  
https://github.com/vulsio/vuls-data-db/pkgs/container/vuls-data-db/versions
