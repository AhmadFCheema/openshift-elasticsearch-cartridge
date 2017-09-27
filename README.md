****
<h1 align="center">
OBSOLETE Project
</h1>

On August 25th, 2017 users were informed of the subsequent [sunset](https://blog.openshift.com/migrate-to-v3-v2-eol/) of OpenShift Online v2 platform by September 30th, 2017 (extended to December 31st, 2017 for paying customers). The next generation v3 platform [replaces](https://docs.openshift.com/enterprise/3.1/release_notes/v2_vs_v3.html#cartridges-vs-images) Cartridges with Images, therefore, making this quick Elasticsearch set-up solution now, unfortunately obsolete. [Comments](https://disqus.com/home/discussion/openshift-blog/get_ready_to_migrate_to_openshift_online_3/) on the "sunset" blog post records some of the incredulity expressed by users on the decision.

This project is kept for archival purposes and any possible benefit it may still provide.
****
# OpenShift Elasticsearch 5.3.2 Cartridge

Downloadable Elasticsearch 5.3.2 cartridge for OpenShift.

To create your scalable Elasticsearch app, run:

````bash
rhc app create <your app name> http://cartreflect-claytondev.rhcloud.com/github/AhmadFCheema/openshift-elasticsearch-cartridge -s
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
export JAVA_HOME=/etc/alternatives/java_sdk_1.8.0; export PATH=$JAVA_HOME/bin:$PATH
elasticsearch/usr/bin/elasticsearch-plugin install <plugin_name>
```
 * The first command directs to the correct Java version (i.e. Java 8).
 * The second command installs the plugin. Plugin names can be found from [here](https://www.elastic.co/guide/en/elasticsearch/plugins/current/index.html). For example: `elasticsearch/usr/bin/elasticsearch-plugin install analysis-icu`.

**OR**

* Clone OpenShift application's git repository (`git clone <OpenShift app SSH URL>`)
* Edit the `plugins.txt` file
* Commit (`git commit -am "new plugin"`)
* Push your changes to OpenShift (`git push`)
 * The current setup first removes *all* previously installed plugins and then installs the ones declared in `plugins.txt`.

## Testing
* The above steps have been tested in OpenShift Online (v2).
* *Adding additional cluster nodes* was not tried.
* Tested on [MediaWiki](https://www.mediawiki.org/wiki/MediaWiki) [1.29.0](https://www.mediawiki.org/wiki/MediaWiki_1.29) [(0e6e155)](https://phabricator.wikimedia.org/rMW0e6e155ea2e708ec99747ba8974a5931a5940727) using Elasticsearch implementation on MediaWiki through [CirrusSearch](https://www.mediawiki.org/wiki/Extension:CirrusSearch) [(0.2)](https://phabricator.wikimedia.org/rECIR7005f38cb56e12c40877036a2b62d35cadd4b324) and [Elastica](https://www.mediawiki.org/wiki/Extension:Elastica) [(1.3.0.0 )](https://phabricator.wikimedia.org/rEELAe2a9593a5097179fbf94c3f4ddd39a7f5590a826) extensions.

## Development
* Development work on this cartridge is detailed at [Elasticsearch 5.3.2 Cartridge (Dev notes)](https://github.com/AhmadFCheema/openshift-elasticsearch-cartridge/wiki/Elasticsearch-5.3.2-Cartridge-(Dev-notes)).

## License
[Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0) and [Criticise not insult](https://islamwiki.org/wiki/islamWiki:Criticise_not_insult).
