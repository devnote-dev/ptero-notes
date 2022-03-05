# Nodes

{% swagger method="get" path="/nodes" baseUrl="https://pterodactyl.domain/api/application" summary="Fetches a list of nodes." %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="include" %}
Available includes: 

`allocations`

, 

`locations`

, 

`page`

, 

`per_page`

, 

`servers`
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
  "object": "list",
  "data": [
    {
      "object": "node",
      "attributes": {
        "id": 1,
        "uuid": "1046d1d1-b8ef-4771-82b1-2b5946d33397",
        "public": true,
        "name": "node 1",
        "description": "first node",
        "location_id": 1,
        "fqdn": "pterodactyl.domain",
        "scheme": "https",
        "behind_proxy": false,
        "maintenance_mode": false,
        "memory": 2048,
        "memory_overallocate": 0,
        "disk": 5000,
        "disk_overallocate": 0,
        "upload_size": 100,
        "daemon_listen": 8080,
        "daemon_sftp": 2022,
        "daemon_base": "/var/lib/pterodactyl/volumes",
        "created_at": "2022-01-12T06:20:00+00:00",
        "updated_at": "2022-01-12T07:14:00+00:00",
        "allocated_resources": {
          "memory": 8192,
          "disk": 20000
        }
      }
    },
    {
      "object": "node",
      "attributes": {
        "id": 2,
        "uuid": "21412d5d-4f65-4ba8-8803-6e1754b9b4e6",
        "public": true,
        "name": "node 2",
        "description": "",
        "location_id": 2,
        "fqdn": "pterodactyl.domain",
        "scheme": "https",
        "behind_proxy": false,
        "maintenance_mode": false,
        "memory": 100,
        "memory_overallocate": 0,
        "disk": 100,
        "disk_overallocate": 0,
        "upload_size": 100,
        "daemon_listen": 8080,
        "daemon_sftp": 2022,
        "daemon_base": "/var/lib/pterodactyl/volumes",
        "created_at": "2022-02-22T03:00:40+00:00",
        "updated_at": "2022-02-23T01:12:00+00:00",
        "allocated_resources": {
          "memory": 8192,
          "disk": 20000
        }
      }
    }
  ],
  "meta": {
    "pagination": {
      "total": 2,
      "count": 2,
      "per_page": 50,
      "current_page": 1,
      "total_pages": 1,
      "links": {}
    }
  }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/nodes/{id}" baseUrl="https://pterodactyl.domain/api/application" summary="Fetches a specific node by its ID." %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" type="Integer" required="true" name="id" %}
The ID of the node.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
  "object": "node",
  "attributes": {
  "id": 1,
  "uuid": "1046d1d1-b8ef-4771-82b1-2b5946d33397",
  "public": true,
  "name": "node 1",
  "description": "first node",
  "location_id": 1,
  "fqdn": "pterodactyl.domain",
  "scheme": "https",
  "behind_proxy": false,
  "maintenance_mode": false,
  "memory": 2048,
  "memory_overallocate": 0,
  "disk": 5000,
  "disk_overallocate": 0,
  "upload_size": 100,
  "daemon_listen": 8080,
    "daemon_sftp": 2022,
    "daemon_base": "/var/lib/pterodactyl/volumes",
    "created_at": "2022-01-12T06:20:00+00:00",
    "updated_at": "2022-01-12T07:14:00+00:00",
    "allocated_resources": {
      "memory": 8192,
      "disk": 20000
    }
  }
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="" %}
```javascript
{
    "errors": [
        {
            "code": "NotFoundHttpException",
            "status": "404",
            "detail": "The requested resource does not exist on this server."
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/nodes/{id}/configuration" baseUrl="https://pterodactyl.domain/api/application" summary="Fetches the configuration of a specific node." %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="Integer" required="true" %}
The ID of the node.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "debug": false,
    "uuid": "21412d5d-4f65-4ba8-8803-6e1754b9b4e6",
    "token": "no4itgJ4NIOhbjkn8T4G6Hboiug4Hb5hy65dpoguMEROH4Jfmog8",
    "api": {
        "host": "0.0.0.0",
        "port": 8080,
        "ssl": {
            "enabled": true,
            "cert": "/etc/letsencrypt/live/pterodactyl.domain/fullchain.pem",
            "key": "/etc/letsencrypt/live/pterodactyl.domain/privkey.pem"
        },
        "upload_limit": 100
    },
    "system": {
        "data": "/var/lib/pterodactyl/volumes",
        "sftp": {
            "bind_port": 3033
        }
    },
    "allowed_mounts": [],
    "remote": "https://pterodactyl.domain"
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="" %}
```javascript
{
    "errors": [
        {
            "code": "NotFoundHttpException",
            "status": "404",
            "detail": "The requested resource does not exist on this server."
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/nodes/{id}/allocations" baseUrl="https://pterodactyl.domain/api/application" summary="Fetches a list of allocations on a specific node." %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="Integer" required="true" %}
The ID of the node.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="include" type="String" %}
Available includes: 

`node`

, 

`page`

, 

`per_page`

, 

`save`
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
  "object": "list",
  "data": [
    {
      "object": "allocation",
      "attributes": {
        "id": 1,
        "ip": "45.86.168.218",
        "alias": null,
        "port": 25565,
        "notes": null,
        "assigned": true
      }
    },
    {
      "object": "allocation",
      "attributes": {
        "id": 2,
        "ip": "45.86.168.218",
        "alias": null,
        "port": 25566,
        "notes": "Votifier",
        "assigned": true
      }
    },
    {
      "object": "allocation",
      "attributes": {
        "id": 3,
        "ip": "45.86.168.218",
        "alias": null,
        "port": 25567,
        "notes": null,
        "assigned": false
      }
    },
    {
      "object": "allocation",
      "attributes": {
        "id": 4,
        "ip": "45.86.168.218",
        "alias": null,
        "port": 25568,
        "notes": null,
        "assigned": false
      }
    },
    {
      "object": "allocation",
      "attributes": {
        "id": 5,
        "ip": "45.86.168.218",
        "alias": null,
        "port": 25569,
        "notes": null,
        "assigned": false
      }
    },
    {
      "object": "allocation",
      "attributes": {
        "id": 6,
        "ip": "45.86.168.218",
        "alias": null,
        "port": 25570,
        "notes": null,
        "assigned": false
      }
    },
    {
      "object": "allocation",
      "attributes": {
        "id": 8,
        "ip": "10.0.0.1",
        "alias": null,
        "port": 25565,
        "notes": null,
        "assigned": false
      }
    },
    {
      "object": "allocation",
      "attributes": {
        "id": 9,
        "ip": "45.86.168.218",
        "alias": null,
        "port": 25571,
        "notes": null,
        "assigned": false
      }
    },
    {
      "object": "allocation",
      "attributes": {
        "id": 10,
        "ip": "45.86.168.218",
        "alias": null,
        "port": 25572,
        "notes": null,
        "assigned": false
      }
    },
    {
      "object": "allocation",
      "attributes": {
        "id": 11,
        "ip": "45.86.168.218",
        "alias": null,
        "port": 25573,
        "notes": null,
        "assigned": false
      }
    },
    {
      "object": "allocation",
      "attributes": {
        "id": 12,
        "ip": "45.86.168.218",
        "alias": null,
        "port": 25574,
        "notes": null,
        "assigned": false
      }
    },
    {
      "object": "allocation",
      "attributes": {
        "id": 13,
        "ip": "45.86.168.218",
        "alias": null,
        "port": 25575,
        "notes": null,
        "assigned": false
      }
    },
    {
      "object": "allocation",
      "attributes": {
        "id": 14,
        "ip": "45.86.168.218",
        "alias": null,
        "port": 25576,
        "notes": null,
        "assigned": false
      }
    },
    {
      "object": "allocation",
      "attributes": {
        "id": 15,
        "ip": "45.86.168.218",
        "alias": null,
        "port": 25577,
        "notes": null,
        "assigned": false
      }
    },
    {
      "object": "allocation",
      "attributes": {
        "id": 16,
        "ip": "45.86.168.218",
        "alias": null,
        "port": 25578,
        "notes": null,
        "assigned": false
      }
    },
    {
      "object": "allocation",
      "attributes": {
        "id": 17,
        "ip": "45.86.168.218",
        "alias": null,
        "port": 25579,
        "notes": null,
        "assigned": false
      }
    },
    {
      "object": "allocation",
      "attributes": {
        "id": 18,
        "ip": "45.86.168.218",
        "alias": null,
        "port": 25580,
        "notes": null,
        "assigned": false
      }
    }
  ],
  "meta": {
    "pagination": {
      "total": 17,
      "count": 17,
      "per_page": 50,
      "current_page": 1,
      "total_pages": 1,
      "links": {}
    }
  }
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="" %}
```javascript
{
    "errors": [
        {
            "code": "NotFoundHttpException",
            "status": "404",
            "detail": "The requested resource does not exist on this server."
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/nodes" baseUrl="https://pterodactyl.domain/api/application" summary="Creates a new node." %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="name" type="String" required="true" %}
The name of the node.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="location_id" type="Integer" required="true" %}
The location for the node.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fqdn" type="String" required="true" %}
The FQDN for the node.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="scheme" type="String" required="true" %}
The HTTP scheme for the node.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="memory" type="Integer" required="true" %}
The amount of memory to allocate to the node.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="memory_overallocate" type="Integer" required="true" %}
The amount of overallocated memory to allow on the node.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="disk" type="Integer" required="true" %}
The amount of disk to allocate to the node.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="disk_overallocate" type="Integer" required="true" %}
The amount of overallocated disk to allow on the node.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="upload_size" type="Integer" required="true" %}
The upload size limit for the node.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="daemon_sftp" type="Integer" required="true" %}
The SFTP port to assign to the node.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="daemon_listen" type="Integer" required="true" %}
The daemon port to assign to the node.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
  "object": "node",
  "attributes": {
  "id": 1,
  "uuid": "1046d1d1-b8ef-4771-82b1-2b5946d33397",
  "public": true,
  "name": "node 1",
  "description": "first node",
  "location_id": 1,
  "fqdn": "pterodactyl.domain",
  "scheme": "https",
  "behind_proxy": false,
  "maintenance_mode": false,
  "memory": 2048,
  "memory_overallocate": 0,
  "disk": 5000,
  "disk_overallocate": 0,
  "upload_size": 100,
  "daemon_listen": 8080,
    "daemon_sftp": 2022,
    "daemon_base": "/var/lib/pterodactyl/volumes",
    "created_at": "2022-01-12T06:20:00+00:00",
    "updated_at": "2022-01-12T06:20:00+00:00",
    "allocated_resources": {
      "memory": 8192,
      "disk": 20000
    }
  },
  "meta": {
    "resource": "https://pterodactyl.domain/api/application/nodes/1"
  }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Sent as 422." %}
```javascript
{
    "errors": [
        {
            "code": "ValidationException",
            "status": "422",
            "detail": "<validation message here>" // This changes depending on the invalid field(s).
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/node/{id}/allocations" baseUrl="https://pterodactyl.domain/api/application" summary="Creates an allocation on a specific node." %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="ip" type="String" required="true" %}
The IP for the allocation.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="ports" type="Array" required="true" %}
A list of ports to assign to the allocation.
{% endswagger-parameter %}

{% swagger-response status="204: No Content" description="" %}
```javascript
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Sent as 422." %}
```javascript
{
    "errors": [
        {
            "code": "ValidationException",
            "status": "422",
            "detail": "<validation message here>" // This changes depending on the invalid field(s).
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="patch" path="/nodes/{id}" baseUrl="https://pterodactyl.domain/api/application" summary="Updates a specific node." %}
{% swagger-description %}
Note: 

`PATCH`

 operations require all other fields to update the resource. Those fields can be fetched with a 

`GET`

 request to the resource.
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="Integer" required="true" %}
The ID of the node.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="String" required="true" %}
The name of the node.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="description" type="String" required="true" %}
The description of the node (can be empty).
{% endswagger-parameter %}

{% swagger-parameter in="body" name="location_id" type="Integer" required="true" %}
The location for the node
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fqdn" type="String" required="true" %}
The FQDN for the node.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="scheme" type="String" required="true" %}
The HTTP scheme for the node.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="behind_proxy" type="Boolean" required="true" %}
Whether the node is behind a proxy.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="maintenance_mode" type="Boolean" required="true" %}
Whether the node is on maintenance mode.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="memory" type="Integer" required="true" %}
The amount of memory to allocate to the node.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="memory_overallocate" type="Integer" required="true" %}
The amount of overallocated memory to allow on the node.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="disk" type="Integer" required="true" %}
The amount of disk to allocate to the node.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="disk_overallocate" type="Integer" required="true" %}
The amount of overallocated disk to allow on the node.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="upload_size" type="Integer" required="true" %}
The upload size limit for the node.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="daemon_sftp" type="Integer" required="true" %}
The SFTP port to assign to the node.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="daemon_listen" type="Integer" required="true" %}
The daemon port to assign to the node.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
  "object": "node",
  "attributes": {
  "id": 1,
  "uuid": "1046d1d1-b8ef-4771-82b1-2b5946d33397",
  "public": true,
  "name": "node 1",
  "description": "first node",
  "location_id": 1,
  "fqdn": "pterodactyl.domain",
  "scheme": "https",
  "behind_proxy": false,
  "maintenance_mode": false,
  "memory": 2048,
  "memory_overallocate": 0,
  "disk": 5000,
  "disk_overallocate": 0,
  "upload_size": 100,
  "daemon_listen": 8080,
    "daemon_sftp": 2022,
    "daemon_base": "/var/lib/pterodactyl/volumes",
    "created_at": "2022-01-12T06:20:00+00:00",
    "updated_at": "2022-01-12T07:14:00+00:00",
    "allocated_resources": {
      "memory": 8192,
      "disk": 20000
    }
  }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Sent as 422." %}
```javascript
{
    "errors": [
        {
            "code": "ValidationException",
            "status": "422",
            "detail": "<validation message here>" // This changes depending on the invalid field(s).
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="delete" path="/nodes/{id}" baseUrl="https://pterodactyl.domain/api/application" summary="Deletes a specific node." %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="Integer" required="true" %}
The ID of the node.
{% endswagger-parameter %}

{% swagger-response status="204: No Content" description="The request was successful." %}
```javascript
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="delete" path="/nodes/{id}/allocations/{alloc}" baseUrl="https://pterodactyl.domain/api/application" summary="Deletes an allocation on a specific node." %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="Integer" required="true" %}
The ID of the node.
{% endswagger-parameter %}

{% swagger-parameter in="path" name="alloc" type="Integer" required="true" %}
The ID of the allocation
{% endswagger-parameter %}

{% swagger-response status="204: No Content" description="" %}
```javascript
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="" %}
```javascript
{
    "errors": [
        {
            "code": "NotFoundHttpException",
            "status": "404",
            "detail": "The requested resource does not exist on this server."
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}
