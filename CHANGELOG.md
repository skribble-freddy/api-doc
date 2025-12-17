# Skribble APIs

## Changelog

### Signature Request: Handling for multi-docs

```
	"documents": [
		{
			"id": "{{DOCUMENT_ID_1}}"
		},
		{
			"id": "{{DOCUMENT_ID_2}}"
		}
	],
  "signatures": [
        {
            "sid": "cf392c37-b4e5-7b50-e531-7b447627d979",
            "account_email": "you@example.com",
            "document_signatures": [
                {
                    "document_id": "a84f5085-67e5-e106-71c7-69b3d4b7c632",
                    "visual_signature": null
                },
                {
                    "document_id": "14f65d46-6653-c33c-81a8-260bd5aba3c5",
                    "visual_signature": null
                }
            ],
            "signer_identity_data": {
                "email_address": "you@example.com"
            },
            "sequence": -1,
            "status_code": "OPEN",
            "notify": true,
            "invited_by": "api_production_skribbleag_42b4_9"
        },
    ]
```

### Signature Request: Signing Groups support

```
{
    "signatures": [
        {
            "signer_group_id": "gr_9feb51ba97444c539261b64294f33225",
        }
    ]
}
```

### Signature Request: properties

> Renamed

business to business_id
cc_email_addresses to observers

> New
> origin: "API",
