# OpenShift Elasticsearch 5.2.2 Cartridge

Downloadable Elasticsearch 5.2.2 cartridge for OpenShift.

To create your scalable Elasticsearch app, run:

````bash
rhc app create <your app name> "http://cartreflect-claytondev.rhcloud.com/github/AhmadFCheema/openshift-elasticsearch-cartridge?commit=6b6e13d9ec4a2bb732d53b31687a86093baa88e4" -s
````

**NOTE:** Your app currently must be a scalable app or this cartridge will not run.

## Adding additional cluster nodes
To add more nodes to the cluster, simply add more gears:

````bash
rhc cartridge scale -a <your app name> elasticsearch <number of total gears you want>
````

## Plugins
To install [Elasticsearch plugins](https://www.elastic.co/guide/en/elasticsearch/plugins/current/index.html):

* SSH into your OpenShift application
* Run commands:
```bash
chmod 700 elasticsearch/usr/bin/elasticsearch-plugin
export JAVA_HOME=/etc/alternatives/java_sdk_1.8.0; export PATH=$JAVA_HOME/bin:$PATH
elasticsearch/usr/bin/elasticsearch-plugin install <plugin_name>
```
 * The first command gives permission for running the plugin installation script (needs to be run only once).
 * The second command directs to the correct Java version (i.e. Java 8).
 * The third command installs the plugin. Plugin names can be found from [here](https://www.elastic.co/guide/en/elasticsearch/plugins/current/index.html). For example: `elasticsearch/usr/bin/elasticsearch-plugin install analysis-icu`.

**OR**

* Clone OpenShift application's git repository (`git clone <OpenShift app SSH URL>`)
* Edit the `plugins.txt` file
* Commit (`git commit -am "new plugin"`)
* Push your changes to OpenShift (`git push`)
 * The current setup first removes *all* previously installed plugins and then installs the ones declared in `plugins.txt`.

## Testing
* The above steps have been tested in OpenShift Online (v2).
* *Adding additional cluster nodes* was not tried.
* Tested on [MediaWiki](https://www.mediawiki.org/wiki/MediaWiki) [1.29.0](https://www.mediawiki.org/wiki/MediaWiki_1.29) [(54d0b02)](https://phabricator.wikimedia.org/rMW54d0b02c69b7af3412ef31db45ae0be773d12e77) using Elasticsearch implementation on MediaWiki through [CirrusSearch](https://www.mediawiki.org/wiki/Extension:CirrusSearch) [(0.2)](https://phabricator.wikimedia.org/rECIR7005f38cb56e12c40877036a2b62d35cadd4b324) and [Elastica](https://www.mediawiki.org/wiki/Extension:Elastica) [(1.3.0.0 )](https://phabricator.wikimedia.org/rEELAe2a9593a5097179fbf94c3f4ddd39a7f5590a826) extensions.

## Development
* Development work on this cartridge is detailed at [Elasticsearch 5.2.2 Cartridge (Dev notes)](https://github.com/AhmadFCheema/openshift-elasticsearch-cartridge/wiki/Elasticsearch-5.2.2-Cartridge-(Dev-notes)).

## License
[Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0) and [Criticise not insult](https://islamwiki.org/wiki/islamWiki:Criticise_not_insult).
