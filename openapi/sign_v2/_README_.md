openapi: 3.1.0
info:
  title: Skribble API v2
  version: 2.0.1
  description: >-
    The Skribble API v2 documentation describes the publicly available Skribble
    API version 2. The API allows businesses and teams of any size to integrate
    the e-signing solution of Skribble with internal systems, software, or SaaS
    solutions. It provides a simple interface to create and manage signature
    requests programmatically. Signature requests define who signs what and
    describe the document flow between participants. Actual signing occurs in
    the Skribble web application.

    To get started, set up Skribble Business. Feedback and questions can be sent
    to the Google Group public-api-users@skribble.com.

    API v2 provides enhanced features including creating, finding, and
    triggering signature requests, user and monitoring details, and reporting
    activities. It maintains backward compatibility with API v1 but upgrading is
    recommended to access the latest features. Migration from API v1 involves
    updating base URLs, renaming fields, and adjusting visual signature
    positions.
  license:
    name: Apache 2.0
    identifier: Apache-2.0
    url: https://www.apache.org/licenses/LICENSE-2.0.html
  termsOfService: https://www.skribble.com/en-eu/terms-of-use/
  contact:
    name: Skribble Engineering
    url: https://skribble.com
    email: info@skribble.com
servers:
  - url: https://api.skribble.com/v2
    description: Production - Switzerland
  - url: https://api.skribble.de/v2
    description: Production - Germany
  - url: https://api.scribital.com/v2
    description: Staging - Switzerland
  - url: https://api.scribital.de/v2
    description: Staging - Germany
paths:
  /access/login:
    $ref: paths/v2_access_login.yaml
  /v2/signature-requests:
    $ref: paths/v2_signature-requests.yaml
  /0000...2222:
    $ref: paths/0000...2222.yaml
  /v2/signature-requests/{SR_ID}:
    $ref: paths/v2_signature-requests_{SR_ID}.yaml
  /v2/documents/{DOC_ID}/content:
    $ref: paths/v2_documents_{DOC_ID}_content.yaml
  /v2/sendto/{SEND_TO_ID}/track:
    $ref: paths/v2_sendto_{SEND_TO_ID}_track.yaml
  /sendto/{SEND_TO_ID}/download:
    $ref: paths/sendto_{SEND_TO_ID}_download.yaml
  /v2/documents:
    $ref: paths/v2_documents.yaml
  /v2/documents/{DOC_ID}:
    $ref: paths/v2_documents_{DOC_ID}.yaml
  /v2/documents/{DOC_ID}/pages/{PAGE_ID}:
    $ref: paths/v2_documents_{DOC_ID}_pages_{PAGE_ID}.yaml
  /v2/signature-requests/{SR_ID}/signatures:
    $ref: paths/v2_signature-requests_{SR_ID}_signatures.yaml
  /v2/signature-requests/{SR_ID}/signatures/{SID}:
    $ref: paths/v2_signature-requests_{SR_ID}_signatures_{SID}.yaml
  /v2/signature-requests/{SR_ID}/attachments:
    $ref: paths/v2_signature-requests_{SR_ID}_attachments.yaml
  /v2/signature-requests/{SR_ID}/attachments/{ATTACHMENT_ID}/content:
    $ref: >-
      paths/v2_signature-requests_{SR_ID}_attachments_{ATTACHMENT_ID}_content.yaml
  /v2/signature-requests/{SR_ID}/attachments/{ATTACHMENT_ID}:
    $ref: paths/v2_signature-requests_{SR_ID}_attachments_{ATTACHMENT_ID}.yaml
  /v2/signature-requests/{SR_ID}/withdraw:
    $ref: paths/v2_signature-requests_{SR_ID}_withdraw.yaml
  /v2/sendto/{SEND_TO_ID}:
    $ref: paths/v2_sendto_{SEND_TO_ID}.yaml
  /v2/signature-requests/{SR_ID}/remind:
    $ref: paths/v2_signature-requests_{SR_ID}_remind.yaml
  /v2/seal:
    $ref: paths/v2_seal.yaml
  /v2/sendto:
    $ref: paths/v2_sendto.yaml
  /signature-qualities-detail:
    $ref: paths/signature-qualities-detail.yaml
  /v2/user/signature-qualities:
    $ref: paths/v2_user_signature-qualities.yaml
  /v2/activities/signatures:
    $ref: paths/v2_activities_signatures.yaml
  /v2/signature-requests/{SR_ID}/callbacks:
    $ref: paths/v2_signature-requests_{SR_ID}_callbacks.yaml
  /management/health:
    $ref: paths/management_health.yaml
components:
  securitySchemes:
    bearer:
      type: http
      scheme: bearer
security: []
tags:
  - name: 🔑 Authentication
    description: >-
      In order to use the API of Skribble, you first need to obtain an API key
      with an API user. Both can be accessed inside the API key page inside your
      business profile. From here, you can create and manage your API keys.
      Consult our
      [guide](https://docs.skribble.com/business-admin/api/apicreate.html) for
      help.


      Skribble offers two types of API keys:


      **Demo API keys**  

      Demo API keys are for testing and development purposes.  

      You can recognize these keys by their name, which start with
      **api_demo**.  

      Signatures requested by such keys don't have any legal weight and are free
      of charge.


      **Production API keys**  

      Production API keys are used for live systems.  

      Signatures requested by such keys will be invoiced.  

      You can recognize these keys by their name, which usually starts with
      **api_production** or in some rare cases just with **api_prod**.


      > **⚠ Note**  

      All costs of signature requests created with your API keys will be
      **charged to your business**! 
        

      We recommend you to **start with a demo API key for development and
      testing** and switch to the production API key as soon as you are finished
      with testing.


      If you have problems setting up Skribble Business, just drop us an e-mail
      at  

      [info@skribble.com](https://mailto:info@skribble.com)
  - name: 1. Create a SignatureRequest
    description: >-
      The document workflow is quite easy.  

      You have one document and need one or more signatures. The document is
      private and not publicly available.


      We need to create a `SignatureRequest` object in Skribble. A
      `SignatureRequest` is a description telling Skribble, **who** is going to
      sign **what** and optionally how the signature should look like.


      So, let's start with the minimal information Skribble needs.


      1. Tell the user, **what will be signed**  
          The `title` should be short and treated like a file name. This field is mandatory.
          
      2. Tell Skribble **who will sign**  
          The `signatures` array contains all signers of the document.  
          In the example, we have 3 signers. They can sign in any sequence they want, and the signature position and appearance will be defined by the Skribble web application.  
          All participants are informed at the same time and are allowed to sign the document in any order. The system ensures that the document is nevertheless only changed sequentially.  
          The `account_email` contains the user's e-mail address. It has two functions. All notifications are sent to this e-mail address AND the e-mail is used to find the user's ID in our database.
          
      3. Tell Skribble **which document will be signed**  
          The `content` field contains the **Base64 encoded** bytes of the **PDF document**.  
          As an alternative to the `content`, you can give Skribble an URL using the field `file_url`, where it can download the document. The URL must not be used together with the content field.  
          All URLs passed to Skribble must use the HTTPS protocol.  
          `"file_url" : "https://myapp.com/path/to/document"`
          

      > Since we have a private document the recommended way is to transfer it
      to Skribble directly. 
        
      > The **maximum document size** is about **40 MB**, which results in the
      maximum request size of 60 MB. 
        

      You will find more details to the `SignatureRequest` in the chapter
      **Reference**.
  - name: 2. Redirect the user to the Skribble web application
    description: >-
      The user has to visit the [Skribble web
      application](https://my.skribble.com) to actually sign the document.


      When we created a Signature Request, the user got notified by Skribble
      that there is a document waiting to be signed.


      Now we want to continue immediately and redirect the browser directly to
      Skribble showing the uploaded document.


      Skribble provides a `signing_url` inside the SignatureRequest.  

      The `signing_url` not only points to the [Skribble web
      application](https://my.skribble.com), but will directly open the document
      for signing provided that the user is known to Skribble and is logged in.
      Otherwise, the user must login or register first to be able to see the
      document.


      There are some more options available to tailor the signing flow to your
      application's specific needs.


      #### Using redirections


      After successfully signing the document, the user will stay on the
      [Skribble web application](https://my.skribble.com).


      However, you can add three different exit points as query parameters to
      the `signing_url`. Skribble will respect these parameters and redirect the
      user to the provided URLs once the signature process is finished.


      Using this, you can bring the user back from Skribble to your application.


      Make sure you encode your exit URLs properly. This is especially important
      for `GET` parameter separators like **?** and **&** to ensure that they
      are not interpreted by browsers as `GET` parameters on Skribble's web
      application itself.


      ##### Exit points


      | Parameter | Description |

      | --- | --- |

      | `exitURL` | URL to redirect the user to after the signature process
      finished. |

      | `errorURL` | URL to redirect the user to if any error occurs. Defaults
      to exitURL. Ignored if exitURL is not specified. |

      | `declineURL` | URL to redirect the user to if the user declines the
      signature request. Defaults to exitURL. Ignored if exitURL is not
      specified. |

      | `declineRedirect=true` (optional) | Use this in combination with
      `declineURL` to redirect directly to the specified `declineURL`. Skribble
      popups after the decline action will be skipped by this. |


      ##### Redirection timeout


      If `exitURL` is specified the user will be automatically redirected to the
      given URL after a successfull signature process. The default **redirection
      timeout is 45 seconds**.


      Using the URL parameter `redirectTimeout` this duration can be adjusted.


      Values equal or lower than 0 will cause the user to be redirected
      instantly, skipping Skribble's success page. For usability reasons the
      duration cannot be longer than 90 seconds. If a value higher than 90 is
      specified, the value will be set to 90.


      ##### Hide download button


      The success screen can be further simplified by hiding the download
      button. This minimises the chances that the user gets side tracked and
      won't follow through to the intended `exitURL`.


      To hide the download button you must specify an `exitURL` as well as
      `hidedownload`. The actual value of `hidedownload` does not matter for it
      to be active.


      Be aware that you have to offer the signed document as a download to the
      user in your application if you hide the download button on Skribble's
      interface.
  - name: 3. Download the signed PDF document
    description: >-
      Now we want to download the signed PDF document. The `SignatureRequest`
      that we created before contains the `document_id`.  

      The document ID is needed to download the document content or in other
      words to download the PDF document.


      We can get the `SignatureRequest` with `GET
      /v2/signature-requests/{SR_ID}`  

      You will find the document ID inside the field `document_id`.


      Finally, we can download the PDF document with a call to `GET
      /v2/documents/{DOC_ID}/content`.


      > **Note**  

      Documents on Skribble are **unchangeable** (immutable).  

      Changes to the document content, like a completed signature, always lead
      to a **NEW** document with a **NEW** ID. This means that the document ID
      you receive after uploading a document, will differ from the ID you
      receive after downloading the document once it is signed . 
        

      You can find ways to get notified about changes on the `SignatureRequest`
      in the chapter **Monitoring**.
  - name: Define the signers
    description: >-
      As mentioned in the **Quickstart** chapter, it is possible to specify the
      number of signers.  

      Please refer to that chapter for an example.


      The following special cases should be mentioned.


      1.  Add the **SAME signer** more than once.

      2.  **NO signer** initially
  - name: Define Visual Signatures
    description: >-
      The visual signature on a PDF document is an optional element that does
      not affect the legal validity of the electronic signature. The decision to
      add a visual signature is at the discretion of the inviter. Including a
      visual signature can maintain the appearance of a handwritten signature
      and provide additional information about the signer.


      If a signature request lacks specific instructions for a visual signature,
      the user can create and place a visual signature anywhere on the document
      using the [Skribble web application](https://my.skribble.com). This
      flexibility mirrors how physical documents handle signature placement,
      where visual hints like "Please sign here" are helpful but not required.


      In the digital world, we have some more options.


      **Multiple visual signatures**


      Visual signatures can be placed multiple times within a document, similar
      to how one might need to sign in various locations on a physical document.
      The advantage of this approach is that the signatory only needs to sign
      once using the [ Skribble web application](https://my.skribble.com). All
      visual signatures in the document are then linked to this single
      electronic signature.
  - name: Provide PDF file to sign
    description: >-
      The **Skribble API** supports different ways of providing the PDF document
      for signing.
  - name: Define the signature quality and legislation
    description: >-
      Skribble supports different levels of signature qualities – the so-called
      e-signature standards. For more information on when to use which
      e-signature standard, visit our
      [website](https://www.skribble.com/signaturestandards/).


      The selected signature quality for the document is determined by two
      parameters: `quality` and `legislation`.


      The parameter `quality` supports the following values:


      | Quality | Description |

      | --- | --- |

      | **QES** | The document must be signed at QES, so every signer must use
      QES. This is the **default** quality. |

      | **AES** | The document should be signed at AES. Signers will use AES, if
      available, otherwise they fall back to QES, if available. |

      | **AES_MINIMAL** | The document will be signed at at least AES, but a
      higher level is preferred. Signers will sign QES, if available, otherwise
      they will use AES. |

      | **SES** | The document will be signed at SES by every signer. |

      | **DEMO** | The document will be signed with a DEMO signature by every
      signer.  <br>**Note:** This signature has **NO** legal binding at
      all.<br>**ALL** `SignatureRequests` that are created using an API demo
      user (*api_demo_example_xyz*) will get this quality by default. |


      > **Note**  

      > The qualities `QES` and `AES_MINIMAL` must provide a `legislation`
      parameter, because the QES is bound to legal regulations, which are
      different in Switzerland and the EU.


      The legislation parameter correspond to the following values:


      | Legislation | Description |

      | --- | --- |

      | **ZERTES** | QES according to the Swiss law. This is the **default**
      legislation. |

      | **EIDAS** | QES according to the EU law. |
  - name: Signing without an account
    description: >-
      It is possible to create a `SignatureRequest` where one or more invited
      participants won't need a [Skribble](https://my.skribble.com) account to
      sign the `SignatureRequest`. Those signers are called
      _**No-Account-Signers (NAS)**_.


      To create a `SignatureRequest` for a user without an account, omit the
      `signatures` array entry for this user and provide the necessary data
      using the `signer_identity_data` element instead.


      | Field | Description | Mandatory |

      | --- | --- | --- |

      | `email_address` | E-mail address of no account signer | yes (for quality
      SES) |

      | `mobile_number` | Mobile number of no account signer | no |

      | `first_name` | First name of no account signer | no |

      | `last_name` | Last name of no accounts signer | no |

      | `provider` | Evidence provider where Skribble can verify the signer's
      identity data. | no |

      | `language` | See **Language parameter** for more information. | no |


      Other settings can be provided as usual, e.g. callback URLs, documents and
      so on.


      Each entry in the `signatures` array will be treated as a distinct
      identity. This means two entries with the same `signer_identity_data` are
      treated as two different identities and require that this person signs the
      document twice.


      Optionally you can combine `signer_identity_data` and `account_email` in
      your requests. In this case, the system checks first if there is a
      Skribble account with the specified e-mail address. If one is found the
      existing Skribble user will be invited to sign the document. Otherwise,
      the specified user in `signer_identity_data` will be invited to sign.


      > 💡 Good to know  

      We recommend this approach of combining `signer_identity_data` and
      `account_email` if you are unsure whether the user has a Skribble
      account.  

      The benefit is that an existing Skribble user will afterwards find the
      SignatureRequest in the **To sign** section of their account on
      my.skribble.com.  

      Conversely, if you invite them using only `signer_identity_data`, the
      document will not appear in their Skribble account, even if they have an
      existing Skribble account. Instead, they will have to access the document
      using the specific link provided in their signature invitation email. 
        

      When the user visits the URL provided in the field `signing_url` inside
      the signature element, he will be forwarded to a special preview page of
      the PDF document and can start the signature process as usual.


      Missing fields like first name and last name can easily be adjusted by the
      signer through the Skribble web client.


      > Please note that you do not mix up the `signing_url` inside the
      `signature` field with the `signing_url` on the top level of the response.
      This contains the default URL for users with a regular
      [Skribble](https://my.skribble.com) account . 
        

      ##### Language parameter


      ###### Browser view


      Skribble will display its content in the user's browser language by
      default. You can change the language by adding a `lang` parameter to the
      `signing_url` when calling the browser.


      > Example for a `lang` parameter  

      _my.skribble.com/view/some-id-000-00000/some-id-fff-fffff?lang=fr_ 
        

      ###### E-mail


      To determine in which language the e-mails are sent to the user, the
      parameter `language` can be added to `signer_identity_data`.


      ###### Supported languages


      Skribble supports the following languages:


      | Code | Language |

      | --- | --- |

      | en | English (default) |

      | de | German |

      | fr | French |
  - name: Define observers
    description: >-
      Skribble allows observers to be added to a `SignatureRequest`. Observers
      are given read access on the `SignatureRequest` and will be notified in
      the same way about activities on the `SignatureRequest` as a signer of the
      `SignatureRequest`.


      > **Note**  

      > The given observers need to have a valid Skribble account. Otherwise the
      email address will not be accepted as valid observer.
  - name: Disable notification e-mails
    description: >-
      Skribble takes over the communication with all participants of a
      `SignatrueRequest`, such as the creator or the different signers. It
      informs the respective participants by e-mail about changes in the status
      of the SR.These notifications are activated by default, but can be
      deactivated by a parameter.
  - name: Define automatic attachments
    description: >-
      When a `SignatureRequest` has been signed by all signers, all signers and
      all observers are notified by email.


      Skribble provides the option to attach two types of attachments
      automatically to this email:


      *   the signed document and

      *   the signature protocol.   


      This can be configured via the business settings, which can be used to
      define that these documents should generally be attached for all
      `SignatureRequests` created by business members.


      Alternatively it is possible to define the attachments on demand per
      `SignatureRequest` by using the `SignatureRequest` field
      `attach_on_success.`
  - name: Define a specific owner
    description: >-
      Generally, all `SignatureRequest` objects are created by an API user, who
      then typically becomes the owner of these objects.


      However, in some specific cases, you might want to designate a business
      member as the owner of a SignatureRequest. For instance, if you have an
      interface for one of your company applications, you may want the
      application user to become the owner of the `SignatureRequest` when they
      initiate a signing process.


      This is possible, but only if two conditions are met:


      1. The user designated as the new owner must have a **valid Skribble
      account.**

      2. The user designated as the new owner must be a **member of the same
      business** as the API user. External users cannot be made owners of a
      SignatureRequest.
          

      > 💡 Good to know  

      Even after changing the owner, the API user will remain a participant of
      the `SignatureRequest` object with read and write access. This allows the
      API user to continue performing actions such as modifying or retrieving
      the `SignatureRequest` object.
  - name: Define a signing sequence
    description: >-
      It may be the case that certain contracts or documents must be signed by
      the signatories in a certain sequence.
  - name: Disable TAN based NAS notifications for SES
    description: >-
      In combination with SES, Skribble offers a straightforward TAN-based
      validation for the email addresses of No-Account-Signers.


      This mechanism can be disabled by setting the field `notify` to `false`
      and additionally using the field `signer_identity_data.identity_reference`
      which can hold a customer generated value for further identtification.


      This means that No-Account-Signers can sign directly without needing the
      additional Skribble TAN process.


      This option enables you to either handle user identification themselves or
      to simply jump in as guarantee for your users.
  - name: Find
    description: >-
      #### Signature state


      A `SignatureRequest` as well as the single `Signatures` can be in
      different states.  

      The state of the `SignatureRequest` can be found in the field
      `status_overall`.  

      The single `Signatures` contains its state ind the field
      `signatures[].status_code`  

      The `SignatureRequest` and the `Signatures` can take one of the following
      states:


      | State | for Signature | for Signature Request |

      | --- | --- | --- |

      | **OPEN** | Waiting for the user to sign a signature. | At least one user
      has not signed or declined his/her signature yet. |

      | **DECLINED** | The user declined to sign. | At least one user declined
      to sign. The signature request failed. |

      | **WITHDRAWN** | The owner has withdrawn the signature request. | The
      owner has withdrawn the signature request. |

      | **SIGNED** | The user signed the document. | All users signed the
      document. The signature request was successfully completed. |

      | *ERROR* | A technical error occurred. | A technical error occurred. The
      signature request cannot be completed. |


      > **Note**  

      > The signature states are managed by the system. It has informal value
      and cannot be changed using the API.
  - name: Add or remove signers
    description: >-
      The Skribble API provides several methods for adding or removing signers
      from a SignatureRequest object. You can add or remove signers individually
      or update multiple signers simultaneously.
  - name: Add or remove attachments
    description: >-
      You may need to provide participants with additional information in the
      form of supplementary documents, such as Terms & Conditions or appendix
      documents.


      In this case, you can use the `attachment` endpoints to provide such
      documents through the `SignatureRequest` to the participants of the
      `SignatureRequest`.


      **Limits by content-type**


      The Skribble API accepts files of the type PDF, image files, Microsoft
      Office files and plain text types.


      Detailed list of the allowed `content_types`:


      - `application/pdf`

      - `application/x-tika-msoffice`

      - `application/x-tika-ooxml`

      - `application/msword`

      -
      `application/vnd.openxmlformats-officedocument.wordprocessingml.document`

      - `application/vnd.ms-word.document.macroEnabled.12`

      - `application/vnd.ms-excel`

      - `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`

      - `application/vnd.ms-excel.sheet.macroenabled.12`

      - `application/vnd.ms-powerpoint`

      -
      `application/vnd.openxmlformats-officedocument.presentationml.presentation`

      - `application/vnd.ms-powerpoint.presentation.macroEnabled.12`

      - `image/gif`

      - `image/jpeg`

      - `image/png`

      - `test/plain`
          

      **Limits by content-size**


      The maximum size of one attachment file is equal to the the **maximum
      document size** of a PDF, which is about **40 MB**, which results in the
      maximum request size of 60 MB.


      **Limits by amount**


      Skribble currently does not limit the number of attachments per
      SignatureRequest. However, if we observe abuse of this service, we will
      take appropriate measures.
  - name: Modify
    description: >-
      Modifications on existing `SignatureRequests` should be handled with
      care.  

      We recommend creating the `SignatureRequests` with all necessary
      information. 
  - name: Triggers
    description: >-
      Triggering actions on SignatureRequests should be handled with care to
      avoid spamming your users or customers.
  - name: Create
    description: >-
      Uploading and affixing an electronic seal to a document takes just one
      call using the `/v2/seal` resource.


      The JSON is similar to the `SignatureRequest`. It requires only the PDF
      document as a Base64 encoded string in the content field.


      Additionally, you can place a visual signature on the document, as
      described in the [Visual
      Signatures](#cb71da67-1dbe-43a6-b74f-405935d88746) chapter of the Skribble
      API documentation, but this is optional.


      An API response from a seal request contains a `document_id` of the newly
      created document with the seal.


      Use the `GET /v2/documents` resource to retrieve the document with the
      electronic seal or reuse it in further signature requests, such as for
      personal electronic signatures.
  - name: User
    description: >-
      The Skribble API provides the resource `/user`. This resource can be used
      to query user data. At the moment, only the endpoint
      `/user/signature-qualities` is offered to query the possible qualities a
      user can use for signing.
  - name: Report
    description: >-
      Activities provide detailled signature usage information for your
      business.
  - name: Callbacks
    description: >-
      The easiest way to get the correct document ID after signing, is to use
      _success_, _update_ and _failure_ callbacks. These callbacks are triggered
      as soon as one of the mentioned events takes place.


      ##### Set callbacks


      To use these callbacks, the corresponding URL that should be called on one
      of the events, can be added to the `SignatureRequest` in one of these
      fields


      | Field | Description |

      | --- | --- |

      | `callback_success_url` | Is triggered when the document has been
      successfully signed by all parties involved. |

      | `callback_update_url` | Is triggered on changes on the
      `SignatureRequest` object like when one person of all involved parties has
      signed. |

      | `callback_error_url` | Is triggered when a person declines the signature
      or when the `SignatureRequest` is withdrawn. |


      > 💡 Good to know  

      Callback URLs will be called using a _POST_ request.  

      Callback URLs will be HTML encoded for the request. So please ensure, that
      your URL does not contain already encoded characters. 
        

      The callback URLs may contain placeholders, which are replaced with the
      current `SignatureRequest` data before the URL is called.


      | Placeholder | Description |

      | --- | --- |

      | `SKRIBBLE_SIGNATURE_REQUEST_ID` | Will be replaced with the
      `SignatureRequest` ID, which triggers the callback. |

      | `SKRIBBLE_DOCUMENT_ID` | Will be replaced with the most recent or final
      document ID, which belongs to the triggering `SignatureRequest`. |

      | `SKRIBBLE_SIGNATURE_ID` | Only after a successful signature, so only for
      `callback_update_url`, this will be replaced with the Signature ID `SID`
      of the signature just made. |


      So, if the success callback triggers, the URL contains the correct
      document ID, which can then be used to retrieve the document.


      ##### TLS Mutual Authentication


      Callbacks support TLS mutual authentication (mTLS). If the callback
      endpoint (your side) asks for a client authentication during the TLS
      handshake, Skribble will authenticate itself with a [X.509 certificate for
      <i>api.skribble.com.</i>](https://www.skribble.com/ext/api/certificates/api.skribble.com.cer)  

      The callback will additionally send the related [root certificate from
      Globalsign](https://www.skribble.com/ext/api/certificates/GlobalSign_Root_CA.cer)
      as certificate authority as well as the related [intermediate certificate
      by Alpha
      SSL](https://www.skribble.com/ext/api/certificates/AlphaSSL_CA.cer) as
      certificate provider.


      ##### Retrials


      _Default:_ If a callback does not respond immediately, e.g. due to a
      **system downtime** on the callback url server (your side), Skribble will
      retry to call to the callback url every **10 minutes for two hours**.
      After this, Skribble will stop its efforts to contact the callback
      endpoint.


      _Retry-After:_ A callback response may contains a `Retry-After` header.
      With this value your system does informs Skribble API to pause retry
      attempts calling the callback URL until this pause time in seconds
      expires.
  - name: System health
    description: >-
      If you need to monitor the responsiveness of the Skribble API, you may
      want to have a look at the `health` resource. It will give you a short
      update about the current status of the system. `status:UP` tells you that
      the system is up and running.
  - name: Appendix
    description: Appendix
