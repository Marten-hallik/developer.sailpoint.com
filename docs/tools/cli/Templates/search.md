---
id: cli-template-search
title: Search Template
pagination_label: CLI Templates Search
sidebar_label: Search
sidebar_position: 10
sidebar_class_name: cli-template-search
keywords: ['cli', 'template', 'search']
description: Learn about the commands you can use to run search templates from the CLI.
slug: /tools/cli/templates/search
tags: ['CLI']
---

Use search templates to run predefined search queries from the CLI.

This is an example of a template file with 3 search templates populated: 

```json
[
  {
    "name": "all-account-unlocks",
    "description": "All account unlocks in the tenant for a given time range",
    "variables": [{"name": "days", "prompt": "Days before today"}],
    "searchQuery": {
      "indices": ["events"],
      "queryType": null,
      "queryVersion": null,
      "query": {
        "query": "(USER_UNLOCK_PASSED AND created:[now-{{days}}d TO now])"
      },
      "sort": [],
      "searchAfter": []
    }
  },
  {
    "name": "all-provisioning-events",
    "description": "All provisioning events in the tenant for a given time range",
    "variables": [{"name": "days", "prompt": "Days before today"}],
    "searchQuery": {
      "indices": ["events"],
      "queryType": null,
      "queryVersion": null,
      "query": {
        "query": "(type:provisioning AND created:[now-{{days}}d TO now])"
      },
      "sort": [],
      "searchAfter": []
    }
  },
  {
    "name": "all-provisioning-events-90-days",
    "description": "All provisioning events in the tenant for a given time range",
    "variables": [],
    "searchQuery": {
      "indices": ["events"],
      "queryType": null,
      "queryVersion": null,
      "query": {
        "query": "(type:provisioning AND created:[now-90d TO now])"
      },
      "sort": [],
      "searchAfter": []
    }
  }
]
```

This is the search template anatomy:

```json
{
  "name": "all-account-unlocks",
```

This is the search template's name. 

It displays in the template list when you run `sail search template`.

You can also provide this name as an argument: `sail search template all-account-unlocks`

```json
  "description": "All account unlocks in the tenant for a given time range"
```

This is the search template's description. 

It displays following the template name in the `sail search template` list.

```json
  "variables": [{"name": "days", "prompt": "Days before today"}],
```

Use variables to dynamically populate values in the following content during command run time. 

For example, the variable in this template is configured so you can choose how many days back you want to search for account unlock events. When you run `sail search template all-account-unlocks`, a prompt displays, `Input Days before today:` The number you enter will then populate anywhere the variable is used in the following object, and then the query runs. 

```json
  "searchQuery": {
    "indices": ["events"],
    "queryType": null,
    "queryVersion": null,
    "query": {
      "query": "(USER_UNLOCK_PASSED AND created:[now-{{days}}d TO now])" },
      "sort": [], "searchAfter": []
      }
  }
```

Everything inside this searchQuery object matches the standard format of an [Identity Security Cloud search query](https://documentation.sailpoint.com/saas/help/search/building-query.html). A limited number of examples are provided [here](https://developer.sailpoint.com/docs/api/v3/search-post), but the searchQuery object is mapped to the full search object. This means that you can add any search query values missing from this object.
