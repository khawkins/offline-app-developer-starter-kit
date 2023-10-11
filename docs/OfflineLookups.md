# Offline Lookups

[The offline lookups example](../force-app/main/default/lwc/createContactRecord) in Starter Kit demonstrates the capability to search a list of objects (e.g., accounts) when creating/updating a record (e.g., contact) for mobile offline app. When device is online, the lookup field searches records by making network calls. When offline, it searches records from cache. In order to have records available for search offline, they need to be downloaded during briefcase priming. In addition to primed records, any existing drafts can also be searched in offline.

In the example of createContactRecord LWC, a lookup field is added as a base component `lightning-record-picker`  in the HTML file. Upon clicked on the field, a modal page will be presented where use can type a key word to search a list of accounts while creating a contact record. 

```xml
<lightning-record-picker
    label="Account"
    placeholder="Search Accounts..."
    object-api-name="Account"
    value={account}
    onchange={handleChange}
>
</lightning-record-picker>
```

In the component’s JS file, the `handleChange` is called with the selected recordId after an account is selected. The recordId can then be used later when the edit form is submitted.

[The developers document](https://developer.salesforce.com/docs/component-library/bundle/lightning-record-picker/documentation) contains more details on how to use the lightning-record-picker component.

> **Note**
> This component is a Beta Service in Winter'24 release. It is targeted to be GA in the coming releases. [Release Notes](https://help.salesforce.com/s/articleView?id=release-notes.rn_lwc_components.htm&release=246&type=5)

## Steps

1. [Configure your Offline Briefcase](https://github.com/salesforce/offline-app-developer-starter-kit#define-an-offline-briefcase) with the desired objects. In this example, you want to have records to be primed for Contact and Account objects. Especially, the primed account records will be searched when user lookup accounts in offline.

2. At the minimum, deploy the following LWCs to the org which can be added as quick actions to objects
    - viewAccountRecord (Account.view), viewContactRecord (Contact.view)
    - createAccountRecord (Account.create), createContactRecord (Contact.create)

3. Login to the Mobile Offline App. Let the briefcase priming is fully completed.

4. To verify that you can create records while offline:

    1. Turn off the network on your device (e.g. by putting it in Airplane Mode, turning off WiFi, etc.).
    2. Tap the `New` button from the `Contacts` home page to create a new contact.
    3. Fill in the required data fields, like Last Name.
    4. Tap the `Account` lookup field at the bottom. It will bring up a modal page with a search box.
    5. Start searching by entering your filter criteria. The dropdown list shows any records matching your filter in the local cache, including the drafts!
    6. Select an `Account` record from the dropdown list. The modal page is automatically closed, and the `Account` record is filled in the lookup field.
    7. Save the record as a new `Contact` draft.
    
5. Turn on the device network, and let the drafts automatically sync up with the server. You should see that a new contact has been created successfully with an associated account!
