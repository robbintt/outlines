# Installing Semantic Mediawiki with Ansible

Requirements:

1. Use old mediawiki production database (upgrade?)
1. Manage installation
1. Manage upgrades
1. Open Source (contribute back for other hackerspaces and other wikis)
1. Manage backups
1. Testable processes
1. Automatically upgrade/configure/manage semantic mediawiki extension and other extensions


## Requirements

1. We want to use our old database.
1. It would be nice to use [semantic mediawiki](https://www.semantic-mediawiki.org/wiki/Semantic_MediaWiki).
1. We should be able to upgrade and add extensions by redeploying the ansible playbook (idempotency retained)
1. We should install all this stuff with `composer`
	- The Ansible [Composer Module](http://docs.ansible.com/ansible/latest/composer_module.html) is a preview and doesn't guarantee a backwards compatible API. This should be fine.
	- Composer Install Guide: [Install Semantic MediaWiki using Composer](https://vimeo.com/82255034)
	- General [Semantic MediaWiki Install Guide](https://www.semantic-mediawiki.org/wiki/Help:Installation)
	- Semantic Mediawiki [Source](https://github.com/SemanticMediaWiki/SemanticMediaWiki)
	- Abount [Semantic MediaWiki](https://www.semantic-mediawiki.org/wiki/Help:Introduction_to_Semantic_MediaWiki)

## Questions

- What RDBMS are we using now?
- What WikiMedia version are we using now?
- What WikiMedia extensions are we using now?
- How does the wiki upgrade process work?  Special Considerations?


## Alternatives to our own ansible playbook

WikiMedia has an initiative to simplify wiki deployments called [CloudVPS](https://wikitech.wikimedia.org/wiki/Portal:Cloud_VPS).

It is OpenStack powered infrastructure. We want to self-host, but might be able to use their images?


## A Noisebridge Wiki Upgrade Plan

Patrick: "no more snowflakes"

### Trent's Plan

1. Use my `servers.yml` playbook as a base, available [here](https://github.com/robbintt/patternbook/).
2. Add a premade playbook
3. Make significant modifications to accomodate our needs



## Hunting for a premade role


### Success? Google Search

A google search for "ansible role semantic mediawiki" seemed promising and is summarized below. 

There are probably more results available by trying more searches.


#### EMWCon Spring 2017

Found here: [Using Ansible to create and manage a wiki/wiki farm examples](https://www.mediawiki.org/wiki/EMWCon_Spring_2017).

- [Very Promising Playbooks from phabricator.mediawiki.org](https://phabricator.wikimedia.org/diffusion/1881/)
	- [author: Cindy.cicalese](https://www.mediawiki.org/wiki/User:Cindy.cicalese)
- [Not as promising playbooks from meza](https://github.com/enterprisemediawiki/meza/tree/master/src/playbooks)
	- it's just old, don't ignore it outright...


#### BlueSpice Enterprise

This may be helpful to look over.

- They have used ansible to [deploy their enterprise product](https://smw-cindykate.com/main/Component_947846).
- A [BlueSpice Playbook](https://github.com/LinuxCompetenceCenter/BlueSpice-Extensions).
- 

### Some Random Playbooks/Roles

- has releases this year: [github.com/yongxinL/ansible-mediawiki](https://github.com/yongxinL/ansible-mediawiki)
- OLD: [https://github.com/quimgil/ansible-playbook](https://github.com/quimgil/ansible-playbook)
	- derivative: [https://github.com/freephile/ansible-playbook](https://github.com/freephile/ansible-playbook)


### Failed: Ansible Galaxy

The playbooks I found here were incomplete and outdated, as usual.


## Extra

- [ToolForge](https://wikitech.wikimedia.org/wiki/Portal:Toolforge)

	> a hosting environment for developers working on services that provide value to the Wikimedia movement. These services allow developers to easily do ad hoc analytics, administer bots, run webservices, and generally create tools to help editors and other volunteers in their work. The environment also includes access to a variety of data services.




## References

- [wikimedia production environment guidelines](https://wikitech.wikimedia.org/wiki/Help:Development_recommendations_for_easily_moving_to_production)