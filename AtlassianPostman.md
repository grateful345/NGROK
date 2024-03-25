curl --request GET \
  --url 'https://api.atlassian.com/admin/v1/orgs/{Org ID}' \
  --header 'Authorization: Bearer ATATT3xFfGF0J4J8PCmMOw_gQMA_ZEHoiIZRuSMXjIDfwFbFW8W25D0eDdlHMZAQQOj33ZUzfDir1nNi8AGouP58aeQqtUr1KWmAAdgMAe0flA3hZGMg1h4yT_OEaOVc7tBXeJGl2kT3-nYYNFR3T9KLOpZ_PWms_UMhUf-NXY2zgcu2T5vtnbE=7AC97CC5' \
  --header 'Accept: application/json'

https://api.atlassian.com/admin/<version>/orgs/<resource-name>

{
  "info": {
    "_postman_id": "30316f18-8a72-4ddb-9c0e-1f4ca695cdaf",
    "name": "API for Atlassian Access",
    "schema": "https://schema.getpostman.com/json/collection/v2.0.0/collection.json"
  },
  "item": [
    {
      "name": "Orgs",
      "description": "Orgs APIs",
      "item": [
        {
          "name": "Get organizations",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs",
              "query": [
                {
                  "key": "cursor",
                  "value": "{{cursor}}",
                  "disabled": true,
                  "description": "Sets the starting point for the page of results to return."
                }
              ],
              "variable": []
            },
            "method": "GET",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Accept",
                "value": "application/json"
              }
            ],
            "description": "Returns a list of your organizations (ATATT3xFfGF0J4J8PCmMOw_gQMA_ZEHoiIZRuSMXjIDfwFbFW8W25D0eDdlHMZAQQOj33ZUzfDir1nNi8AGouP58aeQqtUr1KWmAAdgMAe0flA3hZGMg1h4yT_OEaOVc7tBXeJGl2kT3-nYYNFR3T9KLOpZ_PWms_UMhUf-NXY2zgcu2T5vtnbE=7AC97CC5).",
            "auth": {postman api key : PMAK-65fcefd7f279ab0001bc1c91-bea679740eef30d16701cb886564e8d242}
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0J4J8PCmMOw_gQMA_ZEHoiIZRuSMXjIDfwFbFW8W25D0eDdlHMZAQQOj33ZUzfDir1nNi8AGouP58aeQqtUr1KWmAAdgMAe0flA3hZGMg1h4yT_OEaOVc7tBXeJGl2kT3-nYYNFR3T9KLOpZ_PWms_UMhUf-NXY2zgcu2T5vtnbE=7AC97CC5}}"
              }
            }
          },
          "response": []
        },
        {
          "name": "Get an organization by ID",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId",
              "query": [],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "ID of the organization to return",
                  "disabled": false
                }
              ]
            },
            "method": "GET",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Accept",
                "value": "application/json"
              }
            ],
            "description": "Returns information about a single organization by ID",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            }
          },
          "response": []
        }
      ]
    },
    {
      "name": "Users",
      "description": "Orgs Users APIs",
      "item": [
        {
          "name": "Get managed accounts in an organization",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/users",
              "query": [
                {
                  "key": "cursor",
                  "value": "{{cursor}}",
                  "disabled": true,
                  "description": "Sets the starting point for the page of results to return."
                }
              ],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "ID of the organization to query",
                  "disabled": false
                }
              ]
            },
            "method": "GET",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Accept",
                "value": "application/json"
              }
            ],
            "description": "Returns a list of managed accounts in an organization.",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            }
          },
          "response": []
        },
        {
          "name": "Search for users within an organization (available only for the new user management experience)",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/users/search",
              "query": [],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "ID of the organization to query",
                  "disabled": false
                }
              ]
            },
            "method": "POST",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Content-Type",
                "value": "application/json"
              },
              {
                "description": "",
                "disabled": false,
                "key": "Accept",
                "value": "application/json"
              }
            ],
            "description": "Returns a list of users with applied privacy controls in an organization using the new user management experience  ** Learn more about the [new user management experience](https://community.atlassian.com/t5/Atlassian-Access-articles/User-management-for-cloud-admins-just-got-easier/ba-p/1576592).",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            },
            "body": {
              "mode": "raw",
              "raw": "{\n  \"limit\": 20\n}"
            }
          },
          "response": []
        }
      ]
    },
    {
      "name": "Groups",
      "description": "Orgs Groups APIs",
      "item": [
        {
          "name": "Search for groups within an organization (available only for the new user management experience)",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/groups/search",
              "query": [],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "ID of the organization to query",
                  "disabled": false
                }
              ]
            },
            "method": "POST",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Content-Type",
                "value": "application/json"
              },
              {
                "description": "",
                "disabled": false,
                "key": "Accept",
                "value": "application/json"
              }
            ],
            "description": "Returns a list of groups in an organization using the new user management experience  ** Learn more about the [new user management experience](https://community.atlassian.com/t5/Atlassian-Access-articles/User-management-for-cloud-admins-just-got-easier/ba-p/1576592).",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            },
            "body": {
              "mode": "raw",
              "raw": "{\n  \"limit\": 20\n}"
            }
          },
          "response": []
        }
      ]
    },
    {
      "name": "Domains",
      "description": "Domain APIs",
      "item": [
        {
          "name": "Get domains in an organization",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/domains",
              "query": [
                {
                  "key": "cursor",
                  "value": "{{cursor}}",
                  "disabled": true,
                  "description": "Sets the starting point for the page of results to return."
                }
              ],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "ID of the organization to query",
                  "disabled": false
                }
              ]
            },
            "method": "GET",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Accept",
                "value": "application/json"
              }
            ],
            "description": "Returns a list of domains in an organization one page at a time.",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            }
          },
          "response": []
        },
        {
          "name": "Get domain by ID",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/domains/:domainId",
              "query": [],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "ID of the organization the domain belongs to",
                  "disabled": false
                },
                {
                  "key": "domainId",
                  "value": "{{domainId}}",
                  "description": "ID of the domain to return",
                  "disabled": false
                }
              ]
            },
            "method": "GET",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Accept",
                "value": "application/json"
              }
            ],
            "description": "Returns information about a single verified domain by ID.",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            }
          },
          "response": []
        }
      ]
    },
    {
      "name": "Events",
      "description": "Events APIs",
      "item": [
        {
          "name": "Get an audit log of events",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/events",
              "query": [
                {
                  "key": "cursor",
                  "value": "{{cursor}}",
                  "disabled": true,
                  "description": "Sets the starting point for the page of results to return"
                },
                {
                  "key": "q",
                  "value": "{{q}}",
                  "disabled": true,
                  "description": "Single query term for searching events."
                },
                {
                  "key": "from",
                  "value": "{{from}}",
                  "disabled": true,
                  "description": "The earliest date and time of the event represented as a UNIX epoch time in milliseconds."
                },
                {
                  "key": "to",
                  "value": "{{to}}",
                  "disabled": true,
                  "description": "The latest date and time of the event represented as a UNIX epoch time in milliseconds."
                },
                {
                  "key": "action",
                  "value": "{{action}}",
                  "disabled": true,
                  "description": "A query filter that returns events of a specific action type."
                },
                {
                  "key": "actor",
                  "value": "{{actor}}",
                  "disabled": true,
                  "description": "A query filter that returns events by one or more specific actors."
                },
                {
                  "key": "ip",
                  "value": "{{ip}}",
                  "disabled": true,
                  "description": "A query filter that returns events by one or more specific ip addresses."
                }
              ],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "ID of the org",
                  "disabled": false
                }
              ]
            },
            "method": "GET",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Accept",
                "value": "application/json"
              }
            ],
            "description": "Returns an audit log of events from an organization one page at a time.",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            }
          },
          "response": []
        },
        {
          "name": "Get an event by ID",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/events/:eventId",
              "query": [],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "ID of the organization to query",
                  "disabled": false
                },
                {
                  "key": "eventId",
                  "value": "{{eventId}}",
                  "description": "ID of the event to return",
                  "disabled": false
                }
              ]
            },
            "method": "GET",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Accept",
                "value": "application/json"
              }
            ],
            "description": "Returns information about a single event by ID.",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            }
          },
          "response": []
        },
        {
          "name": "Get list of event actions",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/event-actions",
              "query": [],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "ID of the organization to query",
                  "disabled": false
                }
              ]
            },
            "method": "GET",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Accept",
                "value": "application/json"
              }
            ],
            "description": "Returns information localized event actions",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            }
          },
          "response": []
        }
      ]
    },
    {
      "name": "Policies",
      "description": "Policies APIs",
      "item": [
        {
          "name": "Get list of policies",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/policies",
              "query": [
                {
                  "key": "cursor",
                  "value": "{{cursor}}",
                  "disabled": true,
                  "description": "Sets the starting point for the page of results to return."
                },
                {
                  "key": "type",
                  "value": "{{type}}",
                  "disabled": true,
                  "description": "Sets the type for the page of policies to return."
                }
              ],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "ID of the organization to query",
                  "disabled": false
                }
              ]
            },
            "method": "GET",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Accept",
                "value": "application/json"
              }
            ],
            "description": "Returns information about org policies",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            }
          },
          "response": []
        },
        {
          "name": "Create a policy",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/policies",
              "query": [],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "ID of the organization to create policy for",
                  "disabled": false
                }
              ]
            },
            "method": "POST",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Content-Type",
                "value": "application/json"
              }
            ],
            "description": "Create a policy for an org",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            },
            "body": {
              "mode": "raw",
              "raw": ""
            }
          },
          "response": []
        },
        {
          "name": "Get a policy by ID",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/policies/:policyId",
              "query": [],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "ID of the organization to return",
                  "disabled": false
                },
                {
                  "key": "policyId",
                  "value": "{{policyId}}",
                  "description": "ID of the policy to query",
                  "disabled": false
                }
              ]
            },
            "method": "GET",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Accept",
                "value": "application/json"
              }
            ],
            "description": "Returns information about a single policy by ID",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            }
          },
          "response": []
        },
        {
          "name": "Update a policy",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/policies/:policyId",
              "query": [],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "ID of the organization to update policy for",
                  "disabled": false
                },
                {
                  "key": "policyId",
                  "value": "{{policyId}}",
                  "description": "ID of the policy to update",
                  "disabled": false
                }
              ]
            },
            "method": "PUT",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Content-Type",
                "value": "application/json"
              }
            ],
            "description": "Update a policy for an org",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            },
            "body": {
              "mode": "raw",
              "raw": ""
            }
          },
          "response": []
        },
        {
          "name": "Delete a policy",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/policies/:policyId",
              "query": [],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "ID of the organization to create policy for",
                  "disabled": false
                },
                {
                  "key": "policyId",
                  "value": "{{policyId}}",
                  "description": "ID of the policy to delete",
                  "disabled": false
                }
              ]
            },
            "method": "DELETE",
            "header": [],
            "description": "Delete a policy for an org",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            }
          },
          "response": []
        },
        {
          "name": "Add Resource to Policy",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/policies/:policyId/resources",
              "query": [],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "ID of the organization to return",
                  "disabled": false
                },
                {
                  "key": "policyId",
                  "value": "{{policyId}}",
                  "description": "ID of the policy to query",
                  "disabled": false
                }
              ]
            },
            "method": "POST",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Content-Type",
                "value": "application/json"
              }
            ],
            "description": "Adds a resource to an existing Policy",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            },
            "body": {
              "mode": "raw",
              "raw": ""
            }
          },
          "response": []
        },
        {
          "name": "Update Policy Resource",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/policies/:policyId/resources/:resourceId",
              "query": [],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "ID of the organization to return",
                  "disabled": false
                },
                {
                  "key": "policyId",
                  "value": "{{policyId}}",
                  "description": "ID of the policy to query",
                  "disabled": false
                },
                {
                  "key": "resourceId",
                  "value": "{{resourceId}}",
                  "description": "Resource ID",
                  "disabled": false
                }
              ]
            },
            "method": "PUT",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Content-Type",
                "value": "application/json"
              }
            ],
            "description": "Update an existing Policy Resource",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            },
            "body": {
              "mode": "raw",
              "raw": ""
            }
          },
          "response": []
        },
        {
          "name": "Delete Policy Resource",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/policies/:policyId/resources/:resourceId",
              "query": [],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "ID of the organization to return",
                  "disabled": false
                },
                {
                  "key": "policyId",
                  "value": "{{policyId}}",
                  "description": "ID of the policy to query",
                  "disabled": false
                },
                {
                  "key": "resourceId",
                  "value": "{{resourceId}}",
                  "description": "Resource ID",
                  "disabled": false
                }
              ]
            },
            "method": "DELETE",
            "header": [],
            "description": "Delete an existing Policy Resource",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            }
          },
          "response": []
        },
        {
          "name": "Validate Policy",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/policies/:policyId/validate",
              "query": [],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "Organization ID",
                  "disabled": false
                },
                {
                  "key": "policyId",
                  "value": "{{policyId}}",
                  "description": "Policy ID",
                  "disabled": false
                }
              ]
            },
            "method": "GET",
            "header": [],
            "description": "Validate a policy based on specific requirements. For example, Trigger CDEN validation by pushing a task into the SQS dns-validation queue",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            }
          },
          "response": []
        }
      ]
    },
    {
      "name": "Directory",
      "description": "Org Directory APIs",
      "item": [
        {
          "name": "User’s last active dates",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/directory/users/:accountId/last-active-dates",
              "query": [
                {
                  "key": "cursor",
                  "value": "{{cursor}}",
                  "disabled": true,
                  "description": "Cursor to fetch the next page"
                }
              ],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "Your organization is identified by a Unique ID. You get your organization ID and Organization API key simultaneously.",
                  "disabled": false
                },
                {
                  "key": "accountId",
                  "value": "{{accountId}}",
                  "description": "Unique ID of the user's account.\nUse the [Jira User Search API](https://developer.atlassian.com/cloud/jira/platform/rest/v3/api-group-users/#api-rest-api-3-users-search-get) to get the accountId (if Jira is available for your Organization). **Jira APIs use a different [authentication method ](https://developer.atlassian.com/cloud/jira/platform/basic-auth-for-rest-apis/).**\nIf you don’t have Jira, export a .csv of the user list. Learn how to [export users from a site](https://support.atlassian.com/organization-administration/docs/export-users-from-a-site/).",
                  "disabled": false
                }
              ]
            },
            "method": "GET",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Accept",
                "value": "application/json"
              }
            ],
            "description": "**Additional response parameters of the API (for e.g., `added_to_org`) are available only to customers using the new user management experience.** Learn more about the [new user management experience](https://community.atlassian.com/t5/Atlassian-Access-articles/User-management-for-cloud-admins-just-got-easier/ba-p/1576592).\n\nSpecifications:\n- Return a user’s last active date for each product listed in Atlassian Administration.\n- Active is defined as viewing a product's page for a minimum of 2 seconds. \n- The data for the last activity may be delayed by up to 24 hours.\n- If the user has not accessed a product, the `product_access` response field will be empty. \n\nLearn the fastest way to call the API with a detailed [tutorial](https://developer.atlassian.com/cloud/admin/organization/user-last-active-dates/).\n",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            }
          },
          "response": []
        },
        {
          "name": "Remove user access",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/directory/users/:accountId",
              "query": [],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "Your organization is identified by a Unique ID. You get your organization ID and Organization API key simultaneously.",
                  "disabled": false
                },
                {
                  "key": "accountId",
                  "value": "{{accountId}}",
                  "description": "Unique ID of the user's account that you are deleting.\nUse the [Jira User Search API](https://developer.atlassian.com/cloud/jira/platform/rest/v3/api-group-users/#api-rest-api-3-users-search-get) to get the accountId (if Jira is available for your Organization). **Jira APIs use a different [authentication method ](https://developer.atlassian.com/cloud/jira/platform/basic-auth-for-rest-apis/).**\nIf you don’t have Jira, export a .csv of the user list. Learn how to [export users from a site](https://support.atlassian.com/organization-administration/docs/export-users-from-a-site/).",
                  "disabled": false
                }
              ]
            },
            "method": "DELETE",
            "header": [],
            "description": "**The API is available for customers using the new user management experience only.** Learn more about the [new user management experience](https://community.atlassian.com/t5/Atlassian-Access-articles/User-management-for-cloud-admins-just-got-easier/ba-p/1576592).\n\nSpecifications:\n- Remove user access to products listed in Atlassian Administration.\n- Remove users from **Users** and **Groups** in **Directory**.\n- Make product licenses available for active users.\n\nUsers with emails whose domain is claimed can still be found in **Managed accounts** in **Directory**.\n\nLearn the fastest way to call the API with a detailed [tutorial](https://developer.atlassian.com/cloud/admin/organization/remove-user/). \n",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            }
          },
          "response": []
        },
        {
          "name": "Suspend user access",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/directory/users/:accountId/suspend-access",
              "query": [],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "Your organization is identified by a Unique ID. You get your organization ID and Organization API key simultaneously.",
                  "disabled": false
                },
                {
                  "key": "accountId",
                  "value": "{{accountId}}",
                  "description": "Unique ID of the user's account that you are suspending.\nUse the [Jira User Search API](https://developer.atlassian.com/cloud/jira/platform/rest/v3/api-group-users/#api-rest-api-3-users-search-get) to get the accountId (if Jira is available for your Organization). **Jira APIs use a different [authentication method ](https://developer.atlassian.com/cloud/jira/platform/basic-auth-for-rest-apis/).**\nIf you don’t have Jira, export a .csv of the user list. Learn how to [export users from a site](https://support.atlassian.com/organization-administration/docs/export-users-from-a-site/).",
                  "disabled": false
                }
              ]
            },
            "method": "POST",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Accept",
                "value": "application/json"
              }
            ],
            "description": "**The API is available for customers using the new user management experience only.** Learn more about the [new user management experience](https://community.atlassian.com/t5/Atlassian-Access-articles/User-management-for-cloud-admins-just-got-easier/ba-p/1576592).\n\nSpecifications:\n- Suspend user access to products listed in Atlassian Administration.\n- Make product licenses available for active users.\n- Maintain respective users in **Groups** for easy restoration.\n\nLearn the fastest way to call the API with a detailed [tutorial](https://developer.atlassian.com/cloud/admin/organization/suspend-user/).\n",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            }
          },
          "response": []
        },
        {
          "name": "Restore user access",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/directory/users/:accountId/restore-access",
              "query": [],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "Your organization is identified by a Unique ID. You get your organization ID and Organization API key simultaneously.",
                  "disabled": false
                },
                {
                  "key": "accountId",
                  "value": "{{accountId}}",
                  "description": "Unique ID of the user's account that you are suspending.\nUse the [Jira User Search API](https://developer.atlassian.com/cloud/jira/platform/rest/v3/api-group-users/#api-rest-api-3-users-search-get) to get the accountId (if Jira is available for your Organization). **Jira APIs use a different [authentication method ](https://developer.atlassian.com/cloud/jira/platform/basic-auth-for-rest-apis/).**\nIf you don’t have Jira, export a .csv of the user list. Learn how to [export users from a site](https://support.atlassian.com/organization-administration/docs/export-users-from-a-site/).",
                  "disabled": false
                }
              ]
            },
            "method": "POST",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Accept",
                "value": "application/json"
              }
            ],
            "description": "**The API is available for customers using the new user management experience only.** Learn more about the [new user management experience](https://community.atlassian.com/t5/Atlassian-Access-articles/User-management-for-cloud-admins-just-got-easier/ba-p/1576592).\n\nThis API will:\n- Restore access of an existing user to products listed in Atlassian Administration.\n- Retract the suspend user action.\n\nThis API will not:\n- Restore access to a user when they have access to a product which is breaching it's license limit.\\\nTo make these changes, you will need to [remove users](https://developer.atlassian.com/cloud/admin/organization/rest/api-group-directory/#api-v1-orgs-orgid-directory-groups-groupid-memberships-accountid-delete) from the group or \n[suspend users](https://developer.atlassian.com/cloud/admin/organization/rest/api-group-directory/#api-v1-orgs-orgid-directory-users-accountid-suspend-access-post) that are in the group first.\\\nYou can also [manage your subscription](https://support.atlassian.com/subscriptions-and-billing/resources/) for the breaching product to increase your license limits.\n- Restore access to any user when your organisation has too many products that are breaching their license limits.\n\nLearn the fastest way to call the API with a detailed [tutorial](https://developer.atlassian.com/cloud/admin/organization/restore-user/).\n",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            }
          },
          "response": []
        },
        {
          "name": "Create group",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/directory/groups",
              "query": [],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "Your organization is identified by a Unique ID. You get your organization ID and Organization API key simultaneously.",
                  "disabled": false
                }
              ]
            },
            "method": "POST",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Content-Type",
                "value": "application/json"
              },
              {
                "description": "",
                "disabled": false,
                "key": "Accept",
                "value": "application/json"
              }
            ],
            "description": "**The API is available for customers using the new user management experience only. Learn more about the [new user management experience](https://community.atlassian.com/t5/Atlassian-Access-articles/User-management-for-cloud-admins-just-got-easier/ba-p/1576592).**\n\nThis API will:\n- Create a group in the organization's directory.\n- Create a collection of users that you can use to easily manage permissions, content access, notification schemes, and roles.\n\n**The creation of new groups using existing group names is not permitted.**\n\nLearn the fastest way to call the API with a detailed [tutorial](https://developer.atlassian.com/cloud/admin/organization/create-group/#create-group).\n",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            },
            "body": {
              "mode": "raw",
              "raw": ""
            }
          },
          "response": []
        },
        {
          "name": "Delete group",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/directory/groups/:groupId",
              "query": [
                {
                  "key": "forceIfNotEmpty",
                  "value": "{{forceIfNotEmpty}}",
                  "disabled": true,
                  "description": "Groups cannot be deleted if it contains users, unless `forceIfNotEmpty=true` is provided"
                }
              ],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "Your organization is identified by a Unique ID. You get your organization ID and Organization API key simultaneously.",
                  "disabled": false
                },
                {
                  "key": "groupId",
                  "value": "{{groupId}}",
                  "description": "Unique ID that serves as reference to the group.\nUse the [Jira Group Search API](https://developer.atlassian.com/cloud/jira/platform/rest/v3/api-group-groups/#api-rest-api-3-groups-picker-get) to get the groupId (if Jira is available for your Organization). **Jira APIs use a different [authentication method ](https://developer.atlassian.com/cloud/jira/platform/basic-auth-for-rest-apis/).**\nIf you don’t have Jira, export a .csv of the user list. Make sure to select **pivot to column** when prompted. Learn how to [export users from a site](https://support.atlassian.com/organization-administration/docs/export-users-from-a-site/).",
                  "disabled": false
                }
              ]
            },
            "method": "DELETE",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Accept",
                "value": "application/json"
              }
            ],
            "description": "**The API is available for customers using the new user management experience only. Learn more about the [new user management experience](https://community.atlassian.com/t5/Atlassian-Access-articles/User-management-for-cloud-admins-just-got-easier/ba-p/1576592).**\n\nThis API will:\n- Delete a group from the organization's directory.\n- Delete the permissions, content access, notification schemes, and roles granted to the users.\n\nThis API will not:\n- Delete groups that are synchronized through SCIM. To delete these groups, you will need to delete them within your external identity provider. Learn more about [configuring user provisioning with an identity provider](https://support.atlassian.com/provisioning-users/docs/configure-user-provisioning-with-an-identity-provider/).\n- Delete a group if it’s marked as a [default group](https://support.atlassian.com/user-management/docs/default-groups-and-permissions).\n- Delete `site-admin` group and therefore revoke org-admin role from a user.\n- Delete a group if it contains users (unless forced).\n\nLearn the fastest way to call the API with a detailed [tutorial](https://developer.atlassian.com/cloud/admin/organization/delete-group/#delete-group).\n",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            }
          },
          "response": []
        },
        {
          "name": "Add user to group",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/directory/groups/:groupId/memberships",
              "query": [],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "Your organization is identified by a Unique ID. You get your organization ID and Organization API key simultaneously.",
                  "disabled": false
                },
                {
                  "key": "groupId",
                  "value": "{{groupId}}",
                  "description": "Unique ID that serves as reference to the group.\nUse the [Jira Group Search API](https://developer.atlassian.com/cloud/jira/platform/rest/v3/api-group-groups/#api-rest-api-3-groups-picker-get) to get the groupId (if Jira is available for your Organization). **Jira APIs use a different [authentication method ](https://developer.atlassian.com/cloud/jira/platform/basic-auth-for-rest-apis/).**\nIf you don’t have Jira, export a .csv of the user list. Make sure to select **pivot to column** when prompted. Learn how to [export users from a site](https://support.atlassian.com/organization-administration/docs/export-users-from-a-site/).",
                  "disabled": false
                }
              ]
            },
            "method": "POST",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Content-Type",
                "value": "application/json"
              },
              {
                "description": "",
                "disabled": false,
                "key": "Accept",
                "value": "application/json"
              }
            ],
            "description": "**The API is available for customers using the new user management experience only. Learn more about the [new user management experience](https://community.atlassian.com/t5/Atlassian-Access-articles/User-management-for-cloud-admins-just-got-easier/ba-p/1576592).**\n\nThis API will:\n- Add user to a group.\n- Assign multiple permissions to user at once.\n- Easily manage permissions, content access, notification schemes, and roles.\n\nThis API will not:\n- Make modifications to group memberships that are synchronized through SCIM. To make changes to these memberships, you will need to modify them within your external identity provider. Learn more about [configuring user provisioning with an identity provider](https://support.atlassian.com/provisioning-users/docs/configure-user-provisioning-with-an-identity-provider/).\n- Add a user to a group that gives access to a product which is breaching it's license limit.\\\nTo make these changes, you will need to [remove users](https://developer.atlassian.com/cloud/admin/organization/rest/api-group-directory/#api-v1-orgs-orgid-directory-groups-groupid-memberships-accountid-delete) from the group or\n[suspend users](https://developer.atlassian.com/cloud/admin/organization/rest/api-group-directory/#api-v1-orgs-orgid-directory-users-accountid-suspend-access-post) that are in the group first.\\\nYou can also [manage your subscription](https://support.atlassian.com/subscriptions-and-billing/resources/) for the breaching product to increase your license limits.\n- Add a user to any group when your organisation has too many products that are breaching their license limits.\n\nLearn the fastest way to call the API with a detailed [tutorial](https://developer.atlassian.com/cloud/admin/organization/add-user-to-group/).\n",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            },
            "body": {
              "mode": "raw",
              "raw": ""
            }
          },
          "response": []
        },
        {
          "name": "Remove user from group",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v1/orgs/:orgId/directory/groups/:groupId/memberships/:accountId",
              "query": [],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "Your organization is identified by a Unique ID. You get your organization ID and Organization API key simultaneously.",
                  "disabled": false
                },
                {
                  "key": "groupId",
                  "value": "{{groupId}}",
                  "description": "Unique ID that serves as reference to the group.\nUse the [Jira Group Search API](https://developer.atlassian.com/cloud/jira/platform/rest/v3/api-group-groups/#api-rest-api-3-groups-picker-get) to get the groupId (if Jira is available for your Organization). **Jira APIs use a different [authentication method ](https://developer.atlassian.com/cloud/jira/platform/basic-auth-for-rest-apis/).**\nIf you don’t have Jira, export a .csv of the user list. Make sure to select **pivot to column** when prompted. Learn how to [export users from a site](https://support.atlassian.com/organization-administration/docs/export-users-from-a-site/).",
                  "disabled": false
                },
                {
                  "key": "accountId",
                  "value": "{{accountId}}",
                  "description": "Unique ID of the user's account that you are adding to the group.\nUse the [Jira User Search API](https://developer.atlassian.com/cloud/jira/platform/rest/v3/api-group-users/#api-rest-api-3-users-search-get) to get the accountId (if Jira is available for your Organization). **Jira APIs use a different [authentication method ](https://developer.atlassian.com/cloud/jira/platform/basic-auth-for-rest-apis/).**\nIf you don’t have Jira, export a .csv of the user list. Learn how to [export users from a site](https://support.atlassian.com/organization-administration/docs/export-users-from-a-site/).",
                  "disabled": false
                }
              ]
            },
            "method": "DELETE",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Accept",
                "value": "application/json"
              }
            ],
            "description": "**The API is available for customers using the new user management experience only. Learn more about the [new user management experience](https://community.atlassian.com/t5/Atlassian-Access-articles/User-management-for-cloud-admins-just-got-easier/ba-p/1576592).**\n\nThis API will:\n- Remove user from a group.\n- Remove multiple permissions for user at once.\n- Easily manage permissions, content access, notification schemes, and roles.\n\nThis API will not:\n- Make modifications to group memberships that are synchronized through SCIM. To make changes to these memberships, you will need to modify them within your external identity provider. Learn more about [configuring user provisioning with an identity provider](https://support.atlassian.com/provisioning-users/docs/configure-user-provisioning-with-an-identity-provider/).\n- Modify `site-admin` group and therefore revoke org-admin role from a user.\n\nLearn the fastest way to call the API with a detailed [tutorial](https://developer.atlassian.com/cloud/admin/organization/remove-user-to-group/).\n",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            }
          },
          "response": []
        }
      ]
    },
    {
      "name": "Workspaces",
      "description": "Org Workspaces APIs",
      "item": [
        {
          "name": "Get list of workspaces",
          "request": {
            "url": {
              "protocol": "{{protocol}}",
              "host": "{{host}}",
              "path": "{{basePath}}v2/orgs/:orgId/workspaces",
              "query": [],
              "variable": [
                {
                  "key": "orgId",
                  "value": "{{orgId}}",
                  "description": "Your organization is identified by a Unique ID. You get your organization ID and Organization API key simultaneously.",
                  "disabled": false
                }
              ]
            },
            "method": "POST",
            "header": [
              {
                "description": "",
                "disabled": false,
                "key": "Content-Type",
                "value": "application/json"
              },
              {
                "description": "",
                "disabled": false,
                "key": "Accept",
                "value": "application/json"
              }
            ],
            "description": "A workspace refers to a specific instance of an Atlassian product that is accessed through a unique URL. Whenever a user initiates or adds a new product instance, it results in the creation of a distinct workspace.\n\nThis API will:\n- Return a paginated list of workspaces in a given org\n- Return more details about an organization's products (including product URL).\n",
            "auth": {
              "type": "bearer",
              "bearer": {
                "key": "token",
                "type": "string",
                "value": "{{ATATT3xFfGF0XmLbrkDjnV3mjB9PvJ51M7nyw7NtrmOSYIdoETrVPQ8ewgxGaWGzVt51nPp6XB0gIdv16qB-cSSfsozIvhi3ntzSgkosHJvYnUy9dJ4pGSeDIZwDAqRE2MI23uiBIc_IYx2E9Oumwgxldv8QAHIx5WChVgy_gaYIyXdGbPZPFt8=F92622C1}}"
              }
            },
            "body": {
              "mode": "raw",
              "raw": "{\n  \"limit\": 20\n}"
            }
          },
          "response": []
        }
      ]
    }
  ],
  "variable": [
    {
      "key": "protocol",
      "name": "Protocol",
      "description": "The HTTP Protocol that should be used for this REST API.",
      "type": "string",
      "value": "https"
    },
    {
      "key": "host",
      "name": "Host",
      "description": "The HTTP host that should be used for this REST API.",
      "type": "string",
      "value": "api.atlassian.com"
    },
    {
      "key": "basePath",
      "name": "Base Path",
      "description": "The path, after the host, of the base of the REST API.",
      "type": "string",
      "value": "admin/"
    }
  ]
}
