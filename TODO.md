# Skribble APIs

## TODO's

001. Adjust SR /documents

Inconsistent use of "content", upload should go over Documents
Those endpoints to add, remove documents fine but only if thee is an option to adjust the signers (who, what to sign)
  /signature-requests/{SR_ID}/documents:
  /signature-requests/{SR_ID}/documents/{DOC_ID}:


002. Callbacks

Move from SR base request out into /callbacks to set, get


003. V3 Evidences


003. Update SR

Reconsider offering this with specific update actions like
- Add / Remove Signer
- Add / Remove Document
- Add / Remove Observer
- Add / Remove Permissions
..

### New stuff

- Model unique URLs (Read, Write)


# Ideas

Integrate LLM Button

# Tools

https://www.npmjs.com/package/openapi-to-postmanv2/v/4.20.1

https://redocusaurus.vercel.app/docs/getting-started/Installation
https://github.com/PaloAltoNetworks/docusaurus-openapi-docs
  https://github.com/facebook/docusaurus/issues/10556

## Solutions

https://scalar.com/
https://www.mintlify.com/
https://docs.stoplight.io/
https://readme.com/documentation
https://fumadocs.dev/docs/ui/comparisons

## References to other docs

https://docs.stripe.com/api
https://developer.paypal.com/api/rest/

https://docs.getunleash.io/quickstart
  Docosaurus https://github.com/Unleash/unleash/tree/main/website
https://github.com/RevenueCat/docs