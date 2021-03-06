OpenStack Identity API v3 OS-QUOTAS Extension
============================================

The proposed solution implies storing Quotas in Keystone.
Keystone API will get additional endpoint and set of operations to adjust Quotas for 
various resources for Users and Projects. Keystone DB will be extended with appropriate 
fields to store Quota information. Other Openstack components will be requesting 
resource reservations via Keystone API. 

API
---

The following additional APIs are supported by this extension:

#### Get resource list:
`GET v3/OS-QUOTAS/resources Content-Type application/json Accept application/json`

Response:

    Status: 200 OK

    {
        "resources": [
            "nova.instances",
            "nova.cores",
            "nova.ram",
            "cinder.volumes"
        ]
    }

#### Create resource:
`POST v3/OS-QUOTAS/resources Content-Type application/json Accept application/json`

Response:

    Status: 200 OK
    {
        "resource": {
            "name": "nova.instances",
            "default_limit": 10
        }
    }

#### Get resource:
`GET v3/OS-QUOTAS/resources/[resource-id] Content-Type application/json Accept application/json`

Response:

    Status: 200 OK

    {
        "resource": {
            "name": "nova.instances",
            "default_limit": 10
        }
    }

#### Update resource:
`PATCH v3/OS-QUOTAS/resources/[resource-id] Content-Type application/json Accept application/json`

Request:

    {
        "resource": {
            "name": "nova.instances",
            "default_limit": 10
        }
    }


Response:

    Status: 200 OK

    {
        "resource": {
            "name": "nova.instances",
            "default_limit": 10
        }
    }

#### Delete resource:
`DELETE v3/OS-QUOTAS/resources/[resource-id] Content-Type application/json Accept application/json`

Response:

    Status: 200 OK

#### Get quota list:
`GET v3/OS-QUOTAS/[subject-type]/[subject-id]/quotas Content-Type application/json Accept application/json`

subject-type can be either 'user' or 'project'.

Response:

    Status: 200 OK

    {
        "quotas": [
            {
                "id": "000-id-000",
                "resource_name": "nova.ram",
                "limit": 1024
            },
            {
                "id": "111-id-111",
                "resource_name": "nova.vcpu",
                "limit": 16
            },
        ]
    }


#### Create quota:
`POST v3/OS-QUOTAS/[subject-type]/[subject-id]/quotas Content-Type application/json Accept application/json`

subject-type can be either 'user' or 'project'.

Request:

    {   
        "quota": {
            "resource_name": "nova.ram",
            "limit": 1024
        }
    }

Response:

    Status: 200 OK

    {   
        "quota": {
            "resource_name": "nova.ram",
            "limit": 1024
        }
    }

#### Get quota:
`GET v3/OS-QUOTAS/[subject-type]/[subject-id]/quotas/[quota-id] Content-Type application/json Accept application/json`

subject-type can be either 'user' or 'project'.

Response:

    Status: 200 OK

    {
        "quota": {
            "resource_name": "nova.ram",
            "limit": 1024
        }
    }

#### Update quota:
`PATCH v3/OS-QUOTAS/[subject-type]/[subject-id]/quotas/[quota-id] Content-Type application/json Accept application/json`

subject-type can be either 'user' or 'project'.

Request:

    {
        "quota": {
            "resource_name": "nova.ram",
            "limit": 1024
        }
    }

Response:

    Status: 200 OK

    {
        "quota": {
            "id": "000-id-000",
            "resource-name": "nova.ram",
            "limit": 1024
        }
    }

#### Delete quota:
`DELETE v3/OS-QUOTAS/[subject-type]/[subject-id]/quotas/[quota-id] Content-Type application/json Accept application/json`

subject-type can be either 'user' or 'project'.

Response:

    Status: 200 OK

